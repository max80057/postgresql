基本語法為

substring ( 截取的欄位名稱,第一個位置,第二個位置 ) in  (比對的值)
下面示範：

找出name裡面第一個英文字母是t的資料

Table名稱為Member_info
<table>
<tr>
<td></td>
<td>name</td>
<td>sex</td>
<td>age</td>
</tr>
<tr>
<td>1</td>
<td>ted</td>
<td>M</td>
<td>18</td>
</tr>
<tr>
<td>2</td>
<td>niki</td>
<td>M</td>
<td>18</td>
</tr>
<tr>
<td>3</td>
<td>tina</td>
<td>F</td>
<td>18</td>
</tr>
</table>

Select name,sex,age from member_info where substring(name,1,1) in (‘t’)

Result:
<table>
<tr>
<td></td>
<td>name</td>
<td>sex</td>
<td>age</td>
</tr>
<tr>
<td>1</td>
<td>ted</td>
<td>M</td>
<td>18</td>
</tr>
<tr>
<td>2</td>
<td>tina</td>
<td>F</td>
<td>18</td>
</tr>
</table>
