### 1. client 与 offfset
![[mouseevent-cilent-offset.png]]

图片依然无法正常匹配位置移动？
css要求：
```CSS
.img_content {
	/* 不能添加以下属性 */
	justify-content
	justify-items
	align-content
	align-items
	margin
}

.img_content {
	/* 一定要添加以下属性 */
	position: absolute;
	/* 不能添加以下属性 */
	margin
}
```