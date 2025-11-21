<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<title>大学生公共场合文明行为调查</title>
<meta name="viewport" content="width=device-width,initial-scale=1">
<style>
body{font-family:Arial,Helvetica,sans-serif;margin:0;padding:20px;background:#f7f7f7}
h3{margin:10px 0 6px;font-size:16px}
.btn{background:#0971f1;color:#fff;border:0;padding:10px 20px;border-radius:4px;margin-top:15px}
</style>
</head>
<body>

<h2>大学生公共场合文明行为调查（匿名）</h2>

<!-- 1. 年级 -->
<h3>1. 您的年级</h3>
<label><input type="radio" name="grade" value="大一"> 大一</label><br>
<label><input type="radio" name="grade" value="大二"> 大二</label><br>
<label><input type="radio" name="grade" value="大三"> 大三</label><br>
<label><input type="radio" name="grade" value="大四及以上"> 大四及以上</label>

<!-- 2. 性别 -->
<h3>2. 性别</h3>
<select id="gender">
  <option value="">请选择</option>
  <option>男</option><option>女</option><option>其他</option><option>不愿透露</option>
</select>

<!-- 3. 食堂插队 -->
<h3>3. 过去一个月您在食堂插队的次数</h3>
<label><input type="radio" name="jump" value="0次"> 0次</label><br>
<label><input type="radio" name="jump" value="1次"> 1次</label><br>
<label><input type="radio" name="jump" value="2-3次"> 2-3次</label><br>
<label><input type="radio" name="jump" value="≥4次"> ≥4次</label>

<!-- 4. 清理桌面 -->
<h3>4. 餐后是否主动清理桌面</h3>
<label><input type="radio" name="clean" value="每次都会"> 每次都会</label><br>
<label><input type="radio" name="clean" value="多数会"> 多数会</label><br>
<label><input type="radio" name="clean" value="偶尔"> 偶尔</label><br>
<label><input type="radio" name="clean" value="从不"> 从不</label>

<!-- 5. 公交外放 -->
<h3>5. 在公交/校内班车曾否大声通话或外放音频</h3>
<label><input type="radio" name="noise" value="从未"> 从未</label><br>
<label><input type="radio" name="noise" value="偶尔"> 偶尔</label><br>
<label><input type="radio" name="noise" value="经常"> 经常</label><br>
<label><input type="radio" name="noise" value="每次都如此"> 每次都如此</label>

<!-- 6. 占座现象 -->
<h3>6. 您目睹同学“用物品占座”的频率</h3>
<label><input type="radio" name="seat" value="很常见"> 很常见</label><br>
<label><input type="radio" name="seat" value="偶尔"> 偶尔</label><br>
<label><input type="radio" name="seat" value="很少"> 很少</label><br>
<label><input type="radio" name="seat" value="没见过"> 没见过</label>

<!-- 7. 扔垃圾现象 -->
<h3>7. 校园内随手乱扔垃圾现象您认为</h3>
<label><input type="radio" name="litter" value="非常普遍"> 非常普遍</label><br>
<label><input type="radio" name="litter" value="一般"> 一般</label><br>
<label><input type="radio" name="litter" value="较少"> 较少</label><br>
<label><input type="radio" name="litter" value="几乎没有"> 几乎没有</label>

<!-- 8. 原因（多选） -->
<h3>8. 您认为导致不文明行为的主要原因是（可多选）</h3>
<label><input type="checkbox" name="why" value="家庭教育缺失"> 家庭教育缺失</label><br>
<label><input type="checkbox" name="why" value="学校制度执行弱"> 学校制度执行弱</label><br>
<label><input type="checkbox" name="why" value="从众心理"> 从众心理</label><br>
<label><input type="checkbox" name="why" value="设施不便"> 设施不便</label><br>
<label><input type="checkbox" name="why" value="惩罚力度低"> 惩罚力度低</label>

<!-- 9. 激励方式（多选） -->
<h3>9. 以下哪些方式最能促使您保持文明行为（可多选）</h3>
<label><input type="checkbox" name="how" value="第二课堂学分"> 第二课堂学分奖励</label><br>
<label><input type="checkbox" name="how" value="志愿者提醒"> 现场志愿者提醒</label><br>
<label><input type="checkbox" name="how" value="朋友圈曝光"> 朋友圈曝光</label><br>
<label><input type="checkbox" name="how" value="校纪处分"> 校纪处分</label><br>
<label><input type="checkbox" name="how" value="现金/消费券"> 现金/消费券奖励</label>

<!-- 10. 开放题 -->
<h3>10. 请用一句话写出您对“提升校园公共场合文明”的金点子</h3>
<textarea id="idea" rows="2" style="width:100%"></textarea>

<button class="btn" onclick="submitForm()">提交问卷</button>

<script>
function submitForm(){
  const url = 'https://script.google.com/macros/s/AKfycbxxxxx/exec'; // <= 换成你的 GOOGLE_URL
  const data = {
    grade : document.querySelector('input[name="grade"]:checked')?.value || '',
    gender: document.getElementById('gender').value,
    jump  : document.querySelector('input[name="jump"]:checked')?.value || '',
    clean : document.querySelector('input[name="clean"]:checked')?.value || '',
    noise : document.querySelector('input[name="noise"]:checked')?.value || '',
    seat  : document.querySelector('input[name="seat"]:checked')?.value || '',
    litter: document.querySelector('input[name="litter"]:checked')?.value || '',
    why   : Array.from(document.querySelectorAll('input[name="why"]:checked')).map(e=>e.value).join(','),
    how   : Array.from(document.querySelectorAll('input[name="how"]:checked')).map(e=>e.value).join(','),
    idea  : document.getElementById('idea').value
  };
  fetch(url,{method:'POST',body:new URLSearchParams(data)})
   .then(r=>r.text())
   .then(msg=>alert('提交成功，感谢您的参与！'))
   .catch(err=>alert('提交失败，请检查网络'));
}
</script>
</body>
</html>
