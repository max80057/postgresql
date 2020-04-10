1.安裝可能所需要的工具
 kernel-headers、cpp、glibc-common、libgcc、glibc、glibc-headers、glibc-devel、libgomp、gcc、libstdc++、libstdc++-devel、gcc-c++、tar、imake、autoconf、make、flex、readline、libtermcap、libtermcap-devel、readline-devel、bison、zlib、zlib-devel

2.取得原始碼
登入官方的FTP取得原始碼
這邊安裝的是postgresql-9.3.2版本

cd /usr/src
ftp ftp.postgresql.org
Name 輸入「 anonymous 」
Password 輸入「 name@company.com 」。
ftp> cd ./pub/source/			放原始碼的地方
ftp> cd v9.3.2					進入需要的版本位置
ftp> bin						設定2進位模式
ftp> hash						顯示傳輸細節
ftp> get postgresql-9.3.2.tar.gz	取得
ftp> quit						離開ftp


3.解壓縮
tar -zxv -f postgresql-9.3.2.tar.gz		注意版本不同

4.開始安裝
cd /usr/src/postgresql-9.3.2/			注意版本不同

組態設定的參數可參考： http://www.postgresql.org/docs/9.3/static/install-procedure.html
設定安裝參數

./configure --prefix=/usr/local/postgresql-9.3.2/ --disable-integer-datetimes 

//	--disable-integer-datetimes				不使用integer來紀錄時間
//	--prefix=/usr/local/postgresql-9.3.2/		設定安裝位置


make							編譯
make world						重新編譯核心系統(請小心使用)
make install						安裝
ln -s /usr/local/postgresql-9.3.2 /usr/local/pgsql	創一個link

安裝額外的模組
contrib參考用網站http://www.highgo.com.cn/docs/docs90cn/contrib.html

cd /usr/src/postgresql-9.3.2/contrib/ 
make all							其實等價於make
make install						安裝

5.新增Linux帳戶
新增群組/使用者/密碼
groupadd postgres	
useradd -g postgres postgres	
passwd postgres	
New UNIX password 輸入「 postgres 」	
//	系統會有警告，或要求重複輸入確認，繼續輸入「 postgres 」。	







6.初始化
cd /usr/local/pgsql/									
mkdir -pv /home/postgres/data-9.3.2					
chown postgres:postgres /home/postgres/data-9.3.2		變更權限
ln -s /home/postgres/data-9.3.2 /usr/local/pgsql/data		
su - postgres										以postgres身份登入


cd /usr/local/pgsql/bin	

初始化設定的參數可參考： http://www.postgresql.org/docs/9.3/static/app-initdb.html
./initdb --locale=en_US.UTF-8 --encoding=UTF8 --pgdata=/usr/local/pgsql/data/		

--locale=en_US.UTF-8              選擇默認的語言環境
--encoding=UTF8 								  選擇DB編碼的類型
--pgdata=/usr/local/pgsql/data/   選擇DB存資料的位置


7.環境變數及日誌文件

logout											登出
vim /etc/profile									
最下面加入下列幾行
	PATH=/usr/local/pgsql/bin:$PATH     設定環境變數
	PGDATA=/usr/local/pgsql/data        DB存資料的位置
	PGLOG=/var/log/pgsql.log            LOG的位置
	export PATH PGDATA PGLOG            運行


source /etc/profile									
touch /var/log/pgsql-9.3.2.log							
ln -s /var/log/pgsql-9.3.2.log /var/log/pgsql.log			
chown postgres:postgres /var/log/pgsql-9.3.2.log			
chown -h postgres:postgres /var/log/pgsql.log			

8.修改設定
vim /usr/local/pgsql/data/postgresql.conf						
打開下列兩行的註解並修改
	listen_addresses = '*'        監聽所有IP的請求
	port = 5432										設定port

vim /usr/local/pgsql/data/pg_hba.conf							
註解掉這行
	host    all             all             ::1/128                 trust
加上下面這行(設定可以使用的網段，網段看需求設定，下面列舉3網段)
	host    all             all             192.168.3.0/24          password

9.加入這個service
cp /usr/src/postgresql-9.3.2/contrib/start-scripts/linux /etc/init.d/postgresql-9.3.2	
vim /etc/init.d/postgresql-9.3.2							
這行註解掉
	PGLOG="$PGDATA/serverlog"						
加入這行
	PGLOG="/var/log/pgsql.log"							

chmod 755 /etc/init.d/postgresql-9.3.2						
ln -s /etc/init.d/postgresql-9.3.2 /etc/init.d/postgresql			

 啟動自動執行服務可參考： http://wiki.postgresql.org/wiki/PostgreSQL_on_RedHat_Linux

chkconfig postgresql on									設定開起就啟動

10.啟動postgresql

service postgresql start									啟動
service postgresql status									檢查狀態
//如果沒有啟動的話，請使用下面命令
//	pg_ctl start
//參考網站http://mark528.pixnet.net/blog/post/7267446-pg_ctl-%E5%95%9F%E5%8B%95%E3%80%81%E5%81%9C%E6%AD%A2%E5%92%8C%E9%87%8D%E5%95%9F-postgresql
psql -U postgres										
postgres=# 	ALTER role postgres with password 'postgres';	新增role
postgres=# 	\q										登出postgresql




11.補充

不能啟動的可能
防火牆是否允許通過
存放data的位置，群組、擁有者是否正確
link是否有正確
pg_hba.conf內允許的區網是否有設定錯誤
postgresql.conf內是否有設定允許外部機器連結，port是否有打開
改設定檔後只否有重新啟動服務


linux底下postgres的client端指令
psql -U postgres
用postgres的身份登入


template0=# 					等待指令

\l 							看系統中所有DB
\c 							從現在的DB轉到別的DB，
							EX:		template0=#\c template1  		
							轉到名字template1的DB
							=> template1=#

\dt 							看有哪些TABLE
\d  							看TABLE的結構
\d  template0 				看template0的內容
\di  						看索引
\q 							離開操作模式
