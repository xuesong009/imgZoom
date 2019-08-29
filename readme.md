##1.关键
###1.1 mover偏移量
(鼠标处于mover中间位置)
mover.style.left = event.pageX - out.offsetLeft - mover.clientWidth / 2;
mover.style.top = event.pageY - out.offsetTop - mover.clientHeight / 2;

备注: + 'px';
偏移量修正:
if (x < 0) {//最左边 最小值0
  x = 0;
} else if (x >= out.clientWidth - mover.clientWidth) {
  //最右边 最大值
  x = out.clientWidth - mover.clientWidth;
}
if (y < 0) {//最上边 最小值0
  y = 0;
} else if (y >= out.clientHeight - mover.clientHeight) {
  //最下边 最大值
  y = out.clientHeight - mover.clientHeight;
}

###1.2 大图bigImg偏移量
偏移量修正
if (event.pageX - out.offsetLeft - mover.clientWidth / 2 > x) {
  x = event.pageX - out.offsetLeft - mover.clientWidth / 2;
}
if (event.pageY - out.offsetTop - mover.clientHeight / 2 > y) {
  y = event.pageY - out.offsetTop - mover.clientHeight / 2;
}
偏移量计算
bigPointX = x * bigImg.clientWidth / img.clientWidth;
bigPointY = y * bigImg.clientHeight / img.clientHeight;
bigImg.style.left = -bigPointX + 'px';
bigImg.style.top = -bigPointY + 'px';

###1.3 图片切换
var imgObj = {};
Object.defineProperty(imgObj, 'nth', {
  set: function (val) {
    bigImg.src = img.src = './images/tx0' + val + '.jpg'
  }
});
imgListBox.addEventListener('click', function (event) {
  event = event || window.event;
  if (event.target.tagName.toLowerCase() === 'img') {
    imgNth = event.target.getAttribute('data-src-nth');
    imgObj.nth = imgNth;
    console.log(imgNth);
  }
}, false);