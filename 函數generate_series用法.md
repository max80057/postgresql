實際範例:隨機產生10個row，內容則是不大於32的值<br>
select ceil(random()*32)  as ra32  from generate_series(1,10)<br>
<table>
<tr>
  <td></td>
  <td>ra32</td>
</tr>
<tr>
  <td>1</td>
  <td>12</td>
</tr>
<tr>
  <td>2</td>
  <td>26</td>
</tr>
<tr>
  <td>3</td>
  <td>1</td>
</tr>
<tr>
  <td>4</td>
  <td>28</td>
</tr>
<tr>
  <td>5</td>
  <td>14</td>
</tr>
<tr>
  <td>6</td>
  <td>32</td>
</tr>
<tr>
  <td>7</td>
  <td>13</td>
</tr>
<tr>
  <td>8</td>
  <td>24</td>
</tr>
<tr>
  <td>9</td>
  <td>32</td>
</tr>
<tr>
  <td>10</td>
  <td>17</td>
</tr>
</table>



語法:<br>
select ceil(random()*int) from generate_series(int,int)<br>
參數詳解：
random()		：隨機產生一個0-1的小數
<table>
<tr>
  <td></td>
  <td>random double precision</td>
</tr>
<tr>
  <td>1</td>
  <td>0.866918697487563</td>
</tr>
</table>
ceil(數字)	：取不小於參數的最小整數

generate_series(int,int)	：生成序列，ex:generate_series(1,5)
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
