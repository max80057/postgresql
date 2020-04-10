string_agg()需要在postgresql 9.0以上才可以使用<Br>
隨機產生一組亂數資料<BR>

範例如下:<br>
select string_agg(('{a,b,c,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,x,y,z,1,2,3,4,5,6,7,8,9,0}'::text[])[ceil(random() * 36)], '') FROM generate_series(1, 16);<br>
<table>
<tr>
  <td></td>
  <td>string_agg text</td>
</tr>
<tr>
  <td>1</td>
  <td>82j3d2c22fujz60v</td>
</tr>
</table>


參數詳解：<br>
1.string_agg(Column, text )	：將Column內的所有元素，用text做字串連接<br>
如table名稱為 test_table<br>
如:select string_agg(random_text,'cc') FROM test_table<br>
<table>
<tr>
  <td></td>
  <td>random_text</td>
</tr>
<tr>
  <td>1</td>
  <td>4</td>
</tr>
<tr>
  <td>2</td>
  <td>4</td>
</tr>
<tr>
  <td>3</td>
  <td>1</td>
</tr>
<tr>
  <td>4</td>
  <td>2</td>
</tr>
<tr>
  <td>5</td>
  <td>z</td>
</tr>
<tr>
  <td>6</td>
  <td>2</td>
</tr>
<tr>
  <td>7</td>
  <td>y</td>
</tr>
<tr>
  <td>8</td>
  <td>3</td>
</tr>
<tr>
  <td>9</td>
  <td>3</td>
</tr>
<tr>
  <td>10</td>
  <td>z</td>
</tr>
</table>

Result:
<table>
<tr>
  <td></td>
  <td>string_agg text</td>
</tr>
</table>
<table>
<tr>
  <td>1</td>
  <td>4cc4cc1cc2cczcc2ccycc3cc3ccz</td>
</tr>
</table>

2.random()		：隨機產生一個0-1的小數
<table>
<tr>
  <td></td>
  <td>random double precision</td>
</tr>
<tr>
  <td></td>
  <td>0.866918697487563</td>
</tr>
</table>
3.ceil(數字)	：取不小於參數的最小整數

4.generate_series(int,int)	：生成序列，ex:generate_series(1,5)
<table>
<tr>
  <td></td>
  <td>generate_series integer</td>
</tr>
<tr>
  <td>1</td>
  <td>1</td>
</tr>
<tr>
  <td>2</td>
  <td>2</td>
</tr>
<tr>
  <td>3</td>
  <td>3</td>
</tr>
<tr>
  <td>4</td>
  <td>4</td>
</tr>
<tr>
  <td>5</td>
  <td>5</td>
</tr>
</table>
