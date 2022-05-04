<template>
  <div class="info">
    <h4>설명</h4>
    <p>입력받은 두 수를 연산하여 결과를 보여줍니다.</p>
    <h4>사용법</h4>
    <p>1. 버튼을 눌러 첫번째 숫자를 입력합니다.</p>
    <p>2. 연산자 선택합니다.</p>
    <p>3. 1과 동일한 방법으로 두 번 째 숫자를 입력합니다.</p>
    <p>4. "="를 눌러 수식의 결과를 보여줍니다</p>
    <p>5. 입력된 숫자를 수정할 때는 <img src="@/img/backspace.jpg">를 선택하여 수정할 수 있습니다.</p>
    <p>6. Clear 버튼을 선택하여 전체 입력과정을 초기화할 수 있습니다.</p>
    <h4>주의사항</h4>
    <p>1. 숫자를 먼저 입력하지 않으면 연산자를 선택할 수 없습니다.</p>
    <p>2. 연산자를 하나만 선택할 수 있습니다. 이미 선택된 연산자가 있으면 경고창을 띄웁니다.</p>
    <p>3. 연산자가 입력된 이전의 수는 수정할 수 없습니다.</p>

    <div class="copyright">
      © <a href="mailto:kangshy@gmail.com">Jiyeon Kang</a>
    </div>
  </div>
</template>
<style>
p
{
  margin : 0;
  padding : 4px 10px 4px 30px;
}
.copyright
{
  padding-top : 50px;
  height:80px;
  text-align : center
}
.copyright a 
{
  text-decoration: none;
  font-size : 12px;
}
</style>