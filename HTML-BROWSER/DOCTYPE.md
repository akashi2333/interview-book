# DOCTYPE

`<!DOCTYPE html>`声明告知WEB浏览器页面使用了那种HTML版本，必须位于文档最前面。

## HTML4.01与HTML5之间的差异

在HTML4.01中，<!DOCTYPE>声明需要引用DTD（文档类型声明），因为HTML4.01是基于SGML（标准通用标记语言）。DTD指定了标记语言的规则，确保了浏览器能够正确的渲染内容。

而HTML5不是基于SGML的，因此不要求引用DTD。

## HTML4.01的三种DTD声明

- Strict模式：这个 DTD 包含所有 HTML 元素和属性，但不包括表象或过时的元素（如 font ）。框架集是不允许的。

  `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">`

- Transitional模式：这个 DTD 包含所有 HTML 元素和属性，包括表象或过时的元素（如 font ）。框架集是不允许的。

  `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">`

- Frameset模式：这个 DTD 包含所有 HTML 元素和属性，包括表象或过时的元素（如 font ）。但是允许使用框架集内容。

  `<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">`

