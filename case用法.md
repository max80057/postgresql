基本語法為

欄位名稱 = (case 欄位名稱1=值1 then 值2 else 欄位 
            case 欄位名稱2=值3 then 值4 else 
                  …………………….        end)
一個條件就是case ……. Else ，最後再加上end表示完成，
條件可以一個也可以多個。
下面示範：
我要update年齡為25歲，條件為age原本是18歲的，剩下的不要動


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
<td>19</td>
</tr>
<tr>
<td>3</td>
<td>tina</td>
<td>F</td>
<td>18</td>
</tr>
</table>



Update member_info set age=
(
case when age=18 then 25 else age end
)


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
<td>25</td>
</tr>
<tr>
<td>2</td>
<td>niki</td>
<td>M</td>
<td>19</td>
</tr>
<tr>
<td>3</td>
<td>tina</td>
<td>F</td>
<td>25</td>
</tr>
</table>

