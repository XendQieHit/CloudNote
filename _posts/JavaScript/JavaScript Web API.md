JavaScript Web API 是浏览器提供的内置功能，允许开发者与浏览器进行交互，执行各种任务，如操作DOM、处理用户输入、发送网络请求、管理存储等。以下是一些常见的JavaScript Web API及其使用示例：

### 1. DOM 操作

#### 获取元素
```javascript
// 获取单个元素
const element = document.getElementById('myElement');
const elementByClass = document.querySelector('.myClass');

// 获取多个元素
const elements = document.getElementsByClassName('myClass');
const elementsByTag = document.getElementsByTagName('div');
const elementsByQuery = document.querySelectorAll('.myClass');
```

#### 修改元素
```javascript
// 修改文本内容
element.textContent = '新的文本';

// 修改HTML内容
element.innerHTML = '<strong>新的HTML内容</strong>';

// 修改属性
element.setAttribute('class', 'newClass');
element.removeAttribute('class');

// 添加和删除类
element.classList.add('newClass');
element.classList.remove('oldClass');
element.classList.toggle('activeClass');
```

### 2. 事件处理

#### 添加事件监听器
```javascript
element.addEventListener('click', function(event) {
    console.log('元素被点击了');
});

// 移除事件监听器
element.removeEventListener('click', function(event) {
    console.log('元素被点击了');
});
```

#### 事件对象
```javascript
element.addEventListener('click', function(event) {
    console.log('点击位置:', event.clientX, event.clientY);
    console.log('目标元素:', event.target);
});
```

### 3. 网络请求

#### Fetch API
```javascript
fetch('https://api.example.com/data')
    .then(response => {
        if (!response.ok) {
            throw new Error('网络响应不是200');
        }
        return response.json();
    })
    .then(data => {
        console.log('数据:', data);
    })
    .catch(error => {
        console.error('数据获取失败:', error.message);
    });
```

#### XMLHttpRequest
```javascript
const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://api.example.com/data', true);
xhr.onload = function() {
    if (xhr.status === 200) {
        console.log('数据:', JSON.parse(xhr.responseText));
    } else {
        console.error('请求失败:', xhr.statusText);
    }
};
xhr.onerror = function() {
    console.error('请求失败');
};
xhr.send();
```

### 4. 存储

#### localStorage
```javascript
// 存储数据
localStorage.setItem('key', 'value');

// 获取数据
const value = localStorage.getItem('key');

// 删除数据
localStorage.removeItem('key');

// 清空所有数据
localStorage.clear();
```

#### sessionStorage
```javascript
// 存储数据
sessionStorage.setItem('key', 'value');

// 获取数据
const value = sessionStorage.getItem('key');

// 删除数据
sessionStorage.removeItem('key');

// 清空所有数据
sessionStorage.clear();
```

### 5. 时间和定时器

#### setTimeout
```javascript
setTimeout(() => {
    console.log('3秒后执行');
}, 3000);
```

#### setInterval
```javascript
const intervalId = setInterval(() => {
    console.log('每2秒执行一次');
}, 2000);

// 停止定时器
clearInterval(intervalId);
```

### 6. 表单操作

#### 获取表单数据
```javascript
const form = document.querySelector('form');
form.addEventListener('submit', function(event) {
    event.preventDefault(); // 阻止表单默认提交行为

    const formData = new FormData(form);
    for (let [key, value] of formData.entries()) {
        console.log(key, value);
    }
});
```

### 7. 导航和历史管理

#### window.location
```javascript
// 获取当前URL
const url = window.location.href;

// 跳转到新URL
window.location.href = 'https://example.com';

// 重新加载页面
window.location.reload();
```

#### History API
```javascript
// 添加历史记录条目
history.pushState({ page: 1 }, 'Title 1', '?page=1');

// 替换当前历史记录条目
history.replaceState({ page: 2 }, 'Title 2', '?page=2');

// 监听历史变化
window.addEventListener('popstate', function(event) {
    console.log('历史状态:', event.state);
});
```

### 8. 用户输入和交互

#### 键盘事件
```javascript
document.addEventListener('keydown', function(event) {
    console.log('按键:', event.key);
});

document.addEventListener('keyup', function(event) {
    console.log('释放按键:', event.key);
});
```

#### 鼠标事件
```javascript
document.addEventListener('mousemove', function(event) {
    console.log('鼠标移动:', event.clientX, event.clientY);
});

document.addEventListener('mousedown', function(event) {
    console.log('鼠标按下:', event.button);
});

document.addEventListener('mouseup', function(event) {
    console.log('鼠标释放:', event.button);
});
```

### 9. 多媒体

#### 音频
```javascript
const audio = new Audio('path/to/audio.mp3');
audio.play();
audio.pause();
audio.volume = 0.5; // 设置音量
```

#### 视频
```javascript
const video = document.querySelector('video');
video.play();
video.pause();
video.volume = 0.5; // 设置音量
video.currentTime = 30; // 设置当前播放时间
```

### 10. 其他有用的API

#### Geolocation API
```javascript
navigator.geolocation.getCurrentPosition(function(position) {
    console.log('纬度:', position.coords.latitude);
    console.log('经度:', position.coords.longitude);
}, function(error) {
    console.error('获取地理位置失败:', error.message);
});
```

#### Notifications API
```javascript
if (Notification.permission === 'granted') {
    new Notification('通知标题', {
        body: '通知内容',
        icon: 'path/to/icon.png'
    });
} else if (Notification.permission !== 'denied') {
    Notification.requestPermission().then(function(permission) {
        if (permission === 'granted') {
            new Notification('通知标题', {
                body: '通知内容',
                icon: 'path/to/icon.png'
            });
        }
    });
}
```

### 总结

JavaScript Web API 提供了丰富的功能，帮助开发者与浏览器进行交互，实现各种复杂的前端应用。以上是一些常见Web API的示例，希望对你有所帮助。如果你有具体的需求或问题，可以告诉我，我会尽力提供更详细的帮助。