<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html lang="ja">
<head>
<meta http-equiv="Content-Style-Type" content="text/css">
<meta http-equiv="Content-Script-Type" content="text/javascript">
<title>히프노시스마이크 노래 소트</title>
<script type="text/javascript">
<!--
//*********************************************************
//
// ?価するメンバ?の名前のリスト
//
// この部分を変更して下さい。名前の削除・追加も可?です。
// 名前を引用符(")で括り、コン?(,)で区切って下さい。
// 但し、リストの最後にはコン?を入れてはいけません。
//
//*********************************************************
var namMember = new Array(

"<img src=이미지주소> <br>나니와☆파라다이주</br>",
"<img src=이미지주소> <br>Crush your mic</br>",
"<img src=이미지주소> <br>Femme fatale</br>",
"<img src=이미지주소> <br>Summit of divisions</br>",
"<img src=이미지주소> <br>오하요 이케부쿠로</br>",
"<img src=이미지주소> <br>시노기</br>",
"<img src=이미지주소> <br>파피용</br>",
"<img src=이미지주소> <br>Stella</br>",
"<img src=이미지주소> <br>Hoodstar</br>",
"<img src=이미지주소> <br>Don't pass the mic</br>",
"<img src=이미지주소> <br>Survival of the illest</br>",
"<img src=이미지주소> <br>Once upon a time in shibuya</br>",
"<img src=이미지주소> <br>Private time</br>",
"<img src=이미지주소> <br>Lesson</br>",
"<img src=이미지주소> <br>파티오 토메나이데</br>",
"<img src=이미지주소> <br>Black or white</br>",
"<img src=이미지주소> <br>그대 있음으로 내가 있네</br>",
"<img src=이미지주소> <br>Gimme the mic</br>",
"<img src=이미지주소> <br>미궁벽</br>",
"<img src=이미지주소> <br>샴페인골드</br>",
"<img src=이미지주소> <br>티그리디아</br>",
"<img src=이미지주소> <br>Bad ass temple funky sounds</br>",
"<img src=이미지주소> <br>승가람Bam</br>",
"<img src=이미지주소> <br>Moonlight shadow</br>",
"<img src=이미지주소> <br>One and two, And law</br>",
"<img src=이미지주소> <br>BB's city</br>",
"<img src=이미지주소> <br>War war war</br>",
"<img src=이미지주소> <br>Ikebukuro west game park</br>",
"<img src=이미지주소> <br>Yokohama walker</br>",
"<img src=이미지주소> <br>Break the wall</br>",
"<img src=이미지주소> <br>School of IKB</br>",
"<img src=이미지주소> <br>Requiem</br>",
"<img src=이미지주소> <br>Divison battle anthem</br>",
"<img src=이미지주소> <br>핑크이로노아이</br>",
"<img src=이미지주소> <br>꽃받침</br>",
"<img src=이미지주소> <br>Scramble gamble</br>",
"<img src=이미지주소> <br>Battle battle battle</br>",
"<img src=이미지주소> <br>Shibuya marble texture-PCCS</br>",
"<img src=이미지주소> <br>Shinjuku style</br>",
"<img src=이미지주소> <br>Division rap battle</br>",
"<img src=이미지주소> <br>Alternative rap battle</br>",
"<img src=이미지주소> <br>Gangsta's paradise</br>",
"<img src=이미지주소> <br>Uncrushable</br>",
"<img src=이미지주소> <br>2DIE4</br>",
"<img src=이미지주소> <br>Nausa de zuiqu</br>",
"<img src=이미지주소> <br>The champion</br>",
"<img src=이미지주소> <br>T.D.D Legend</br>",
"<img src=이미지주소> <br>Wrap&rap</br>",
"<img src=이미지주소> <br>G anthem of Y-CITY</br>",
"<img src=이미지주소> <br>베이사이드 스모킹블루</br>",
"<img src=이미지주소> <br>What's my name?</br>",
"<img src=이미지주소> <br>오레가 이치로</br>",
"<img src=이미지주소> <br>선전포고</br>",
"<img src=이미지주소> <br>New star</br>",
"<img src=이미지주소> <br>drops</br>",
"<img src=이미지주소> <br>시나리오라이어</br>",
"<img src=이미지주소> <br>3$even</br>",
"<img src=이미지주소> <br>Death respect</br>",
"<img src=이미지주소> <br>아아, 오사카 dreamin'night</br>",
"<img src=이미지주소> <br>Tragic transister</br>",
"<img src=이미지주소> <br>Own stage</br>",
"<img src=이미지주소> <br>Faces</br>"



);
//*********************************************************

var lstMember = new Array();
var parent = new Array();
var equal = new Array();
var rec = new Array();
var cmp1,cmp2;
var head1,head2;
var nrec;

var numQuestion;
var totalSize;
var finishSize;
var finishFlag;

//変数の初期化+++++++++++++++++++++++++++++++++++++++++++++
function initList(){
var n = 0;
var mid;
var i;

//??トすべき配列
lstMember[n] = new Array();
for (i=0; i<namMember.length; i++) {
lstMember[n][i] = i;
}
parent[n] = -1;
totalSize = 0;
n++;

for (i=0; i<lstMember.length; i++) {
//要素数が２以上なら２分割し、
//分割された配列をlstMemberの最後に加える
if(lstMember[i].length>=2) {
mid = Math.ceil(lstMember[i].length/2);
lstMember[n] = new Array();
lstMember[n] = lstMember[i].slice(0,mid);
totalSize += lstMember[n].length;
parent[n] = i;
n++;
lstMember[n] = new Array();
lstMember[n] = lstMember[i].slice(mid,lstMember[i].length);
totalSize += lstMember[n].length;
parent[n] = i;
n++;
}
}

//保存用配列
for (i=0; i<namMember.length; i++) {
rec[i] = 0;
}
nrec = 0;

//引き分けの結果を保存するリスト
//キ?：リンク始?の値
// 値 ：リンク終?の値
for (i=0; i<=namMember.length; i++) {
equal[i] = -1;
}

cmp1 = lstMember.length-2;
cmp2 = lstMember.length-1;
head1 = 0;
head2 = 0;
numQuestion = 1;
finishSize = 0;
finishFlag = 0;
}

//リストの??ト+++++++++++++++++++++++++++++++++++++++++++
//flag：比較結果
//  -1：左を選択
//   0：引き分け
//   1：右を選択
function sortList(flag){
var i;
var str;

//recに保存
if (flag<0) {
rec[nrec] = lstMember[cmp1][head1];
head1++;
nrec++;
finishSize++;
while (equal[rec[nrec-1]]!=-1) {
rec[nrec] = lstMember[cmp1][head1];
head1++;
nrec++;
finishSize++;
}
}
else if (flag>0) {
rec[nrec] = lstMember[cmp2][head2];
head2++;
nrec++;
finishSize++;
while (equal[rec[nrec-1]]!=-1) {
rec[nrec] = lstMember[cmp2][head2];
head2++;
nrec++;
finishSize++;
}
}
else {
rec[nrec] = lstMember[cmp1][head1];
head1++;
nrec++;
finishSize++;
while (equal[rec[nrec-1]]!=-1) {
rec[nrec] = lstMember[cmp1][head1];
head1++;
nrec++;
finishSize++;
}
equal[rec[nrec-1]] = lstMember[cmp2][head2];
rec[nrec] = lstMember[cmp2][head2];
head2++;
nrec++;
finishSize++;
while (equal[rec[nrec-1]]!=-1) {
rec[nrec] = lstMember[cmp2][head2];
head2++;
nrec++;
finishSize++;
}
}

//片方のリストを走査し終えた後の処理
if (head1<lstMember[cmp1].length && head2==lstMember[cmp2].length) {
//リストcmp2が走査済 - リストcmp1の残りをコピ?
while (head1<lstMember[cmp1].length){
rec[nrec] = lstMember[cmp1][head1];
head1++;
nrec++;
finishSize++;
}
}
else if (head1==lstMember[cmp1].length && head2<lstMember[cmp2].length) {
//リストcmp1が走査済 - リストcmp2の残りをコピ?
while (head2<lstMember[cmp2].length){
rec[nrec] = lstMember[cmp2][head2];
head2++;
nrec++;
finishSize++;
}
}

//両方のリストの最後に到達した場合は
//親リストを更新する
if (head1==lstMember[cmp1].length && head2==lstMember[cmp2].length) {
for (i=0; i<lstMember[cmp1].length+lstMember[cmp2].length; i++) {
lstMember[parent[cmp1]][i] = rec[i];
}
lstMember.pop();
lstMember.pop();
cmp1 = cmp1-2;
cmp2 = cmp2-2;
head1 = 0;
head2 = 0;

//新しい比較を行う前にrecを初期化
if (head1==0 && head2==0) {
for (i=0; i<namMember.length; i++) {
rec[i] = 0;
}
nrec = 0;
}
}

if (cmp1<0) {
str = "Battle No."+(numQuestion-1)+"<br>"+Math.floor(finishSize*100/totalSize)+"% sorted.";
document.getElementById("battleNumber").innerHTML = str;

showResult();
finishFlag = 1;
}
else {
showImage();
}
}

//結果の?示+++++++++++++++++++++++++++++++++++++++++++++++
function showResult() {
var ranking = 1;
var sameRank = 1;
var str = "";
var i;

str += "<table style=\"width:200px; font-size:12px; line-height:120%; margin-left:auto; margin-right:auto; border:1px solid #000; border-collapse:collapse\" align=\"center\">";
str += "<tr><td style=\"color:#ffffff; background-color:#000; text-align:center;\">순위<\/td><td style=\"color:#ffffff; background-color:#000; text-align:center;\">이름<\/td><\/tr>";

for (i=0; i<namMember.length; i++) {
str += "<tr><td style=\"border:1px solid #000; text-align:right; padding-right:5px;\">"+ranking+"<\/td><td style=\"border:1px solid #000; padding-left:5px;\">"+namMember[lstMember[0][i]]+"<\/td><\/tr>";
if (i<namMember.length-1) {
if (equal[lstMember[0][i]]==lstMember[0][i+1]) {
sameRank++;
} else {
ranking += sameRank;
sameRank = 1;
}
}
}
str += "<\/table>";

document.getElementById("resultField").innerHTML = str;
}

//比較する２つ要素の?示+++++++++++++++++++++++++++++++++++
function showImage() {
var str0 = "Battle No."+numQuestion+"<br>"+Math.floor(finishSize*100/totalSize)+"% sorted.";
var str1 = ""+toNameFace(lstMember[cmp1][head1]);
var str2 = ""+toNameFace(lstMember[cmp2][head2]);

document.getElementById("battleNumber").innerHTML = str0;
document.getElementById("leftField").innerHTML = str1;
document.getElementById("rightField").innerHTML = str2;

numQuestion++;
}

//数値を名前（顔文字）に変換+++++++++++++++++++++++++++++++
function toNameFace(n){
var str = namMember[n];

//顔文字を追加する場合は以下のコメントアウトを外す
//namMemberのインデックスと矛盾しないように注意
/*
str += "<br>────<br>";
switch(n) {
//case -1 はサンプルなので削除すること
case -1: str+="（ ´∀｀）";break;
default: str+=""+n;
}
*/
return str;
}
//-->
</script>
<style type="text/css">
<!--
/**********************************************************

 ?のス?イルを変更する場合はここを編集してください。

**********************************************************/
#mainTable{
font-size: 12px;
font-family: '돋움',sans-serif;
text-align: center;
vertical-align: middle;
width: 410px;
margin-left: auto;
margin-right: auto;
border-collapse: separate;
border-spacing: 10px 5px;
}
#leftField{
width: 120px;
height: 150px;
border: 1px solid #000;
}
#rightField{
width: 120px;
height: 150px;
border: 1px solid #000;
}
.middleField{
width: 120px;
height: 70px;
border: 1px solid #000;
}
//-->
<!--
A{
  text-decoration : none;
}
-->
<!--
a:hover{color:#99ccff;}
-->
</style>
<meta name="generator" content="Namo WebEditor(Trial)">
<meta http-equiv="content-type" content="text/html; charset=utf-8"></head>

<body text="#000000" bgcolor="#ffffff" link="#0099ff" vlink="#0099ff" alink="#0099ff">
<table id="mainTable" align="center">
<tr>
        <td id="battleNumber" colspan="3" style="padding-bottom: 10px;">
            <p>&nbsp;</p>
        </td>
</tr>
<tr>
<td id="leftField" onClick="if(finishFlag==0)sortList(-1);" rowspan="2">
&nbsp;
</td>
<td class="middleField" onClick="if(finishFlag==0)sortList(0);">
둘 다 좋다
</td>
<td id="rightField" onClick="if(finishFlag==0)sortList(1);" rowspan="2">
</td>
</tr>
<tr>
<td class="middleField" onClick="if(finishFlag==0)sortList(0);">
모르겠다
</td>
</tr>
</table><br><br>
<div id="resultField" style="text-align:center;">
    <p><font size="2" face="돋움"><span style="">아래에 하고 싶은 말을 적어주세요</font></p>
    <p><font size="2" face="돋움">아래에 하고 싶은 말을 적어주세요</font></p>

</div>
<script type="text/javascript">
<!--
initList();
showImage();
//-->
</script>

</body>
</html>
