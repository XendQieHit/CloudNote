在你要等待的执行函数里将其结构：
```JavaScript
function content() {
	......
}

```
改为：
```JavaScript
function load_content() {
	const promise = new Promise((resolve, reject) => {
		......
		resolve(); // 执行完毕后记得加个这个
		// reject(); // 如果执行出错的话就调用这个，停止这个函数后面的步骤
	});
}
```
使用该example函数实现程序待命：
```JavaScript
//主程序运行空间
async function main() {
	......
	example1();
	example2();
	await load_content(); // 等待
	example3();
	example4();
	......
}
```

实例：
load_content_md.js内部：
```JavaScript
import { getQueryParams } from "../get_queryparam.mjs"; // 获得URL查询字符串
import { loading_animation } from "../loading_animation.mjs";
import { relocateRoot } from "../relocate_root.mjs";
  
const content_md = document.querySelector(".content_md");
const docs_path = relocateRoot(getQueryParams('Path'));
function load_content_md() {

    return new Promise(function(resolve, reject) {

        loading_animation(content_md);
        // 这里接受的形参link是对应md文档转换后的html文件路径
        fetch(docs_path)
        .then(response => {
            if (!response.ok) {
                throw new Error('炸了！');
            }
            return response.text();
        })
        .then(html => {
            // 建立一个缓存操作空间，把html文本放入该空间，使其文本实例化为html元素
            const buffer = document.createElement('div');
            buffer.innerHTML = html;
            const imgs = buffer.querySelectorAll('img');
            // 图片链接地址由相对路径改为绝对路径
            imgs.forEach(img => {
                const buffer = img.src.match(/[^\/]*$/);
                img.src = docs_path + "files/" + buffer;
            });
            content_md.innerHTML = ''; // 初始化加载先清空
            content_md.innerHTML = buffer.innerHTML; // 将缓存库内容应用
            
            resolve();
        })

        .catch(error => {
            content_md.innerHTML = '';
            const h1 = document.createElement('h1');
            const ul = document.createElement('ul');
            const p1 = document.createElement('p');
            const error_hint = ["请求时间超时，重新刷新网页加载试试..？", "文档不存在，核对一下地址输入是否正确..?"];
            h1.textContent = ">_<加载出错了";
            content_md.appendChild(h1);
            p1.textContent = "获取文档内容失败，可能的原因：";
            content_md.appendChild(p1);
            for (let hint of error_hint) {
                const li = document.createElement('li');
                li.textContent = hint;
                ul.appendChild(li);
            }
            content_md.appendChild(ul);

            reject();
        });
    });
}
export { load_content_md };
```
主程序内部：
```JavaScript
import { get_navigation } from "./get_navigation.mjs";
import { load_content_md } from "./load_content_md.mjs";
import { apart_md_content } from "./apart_md_content.mjs";
import { gen_docs_title } from "./gen_docs_title.mjs";
import { zoomify_imgs } from "./zoomify_img.mjs";
import { get_pg_list } from "./get_pg_list.mjs";
import { get_ql_menu } from "./get_ql_menu.mjs";

document.addEventListener('DOMContentLoaded', async function() {

    get_navigation(); // 加载导航栏
    get_ql_menu(); // 加载总目录
    await load_content_md(); // 加载文档内容
    gen_docs_title(); // 更新网页标题
    get_pg_list(); // 加载段落标题栏
    zoomify_imgs();
    apart_md_content(); // 分段文档内容
});
```
这里就会先等load_content_md加载完后再执行后面的函数了。