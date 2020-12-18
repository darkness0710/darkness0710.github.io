# 1. Obfuscated
Đầu tiên để tìm hiểu xem Obfuscated là gì chúng ta ghé qua https://en.wikipedia.org/wiki/Obfuscation_(software) xem a wiki định nghĩa nó là gì.
```
In software development, obfuscation is the deliberate act of creating source or machine code that is difficult for humans to understand. 
Like obfuscation in natural language, it may use needlessly roundabout expressions to compose statements.
Programmers may deliberately obfuscate code to conceal its purpose (security through obscurity) or its logic or implicit values embedded in it,
primarily, in order to prevent tampering, deter reverse engineering, or even as a puzzle or recreational challenge for someone reading the source code.
This can be done manually or by using an automated tool, the latter being the preferred technique in industry.
```
Dài quá, đại khái ý của nó là:
```
Biên dịch các đoạn code ban đầu thành các đoạn code mới sao cho thật khó hiểu và khó đọc (yaoming), dùng mọi thử đoạn như đảo tên biến, xáo trọn hàm,
tóm lại mục đích là để che giấu source code. Biên dịch bằng tool hoặc bằng tay tự viết.
```
# 2. Minified vs Obfuscated
# 2.1 Minified
Trong thực tế, kĩ thuật Minified được áp dụng rộng rãi đặc biệt điển hình như các file thư viện javascript.
Giả sử khi chúng ta sử dụng thư viện **Jquery** và chúng ta sẽ được suggest 2 version chính:
```
Minified: https://code.jquery.com/jquery-3.3.1.min.js
Uncompressed: https://code.jquery.com/jquery-3.3.1.js
```

Với file Uncompressed:

```
/*!
 * jQuery JavaScript Library v3.3.1
 * https://jquery.com/
 *
 * Includes Sizzle.js
 * https://sizzlejs.com/
 *
 * Copyright JS Foundation and other contributors
 * Released under the MIT license
 * https://jquery.org/license
 *
 * Date: 2018-01-20T17:24Z
 */
( function( global, factory ) {

	"use strict";

	if ( typeof module === "object" && typeof module.exports === "object" ) {

		// For CommonJS and CommonJS-like environments where a proper `window`
		// is present, execute the factory and get jQuery.
		// For environments that do not have a `window` with a `document`
		// (such as Node.js), expose a factory as module.exports.
		// This accentuates the need for the creation of a real `window`.
		// e.g. var jQuery = require("jquery")(window);
		// See ticket #14549 for more info.
		module.exports = global.document ?
			factory( global, true ) :
			function( w ) {
				if ( !w.document ) {
					throw new Error( "jQuery requires a window with a document" );
				}
				return factory( w );
			};
	} else {
		factory( global );
	}

// Pass this if window is not defined yet
} 
```

Với file Minified:
```
/*! jQuery v3.3.1 | (c) JS Foundation and other contributors | jquery.org/license */
!function(e,t){"use strict";"object"==typeof module&&"object"==typeof module.exports?module.exports=e.document?t(e,!0):function(e){if(!e.document)throw new Error("jQuery requires a window with a document");return t(e)}:t(e)}("undefined"!=typeof window?window:this,function(e,t){"use strict";var n=[],r=e.document,i=Object.getPrototypeOf,o=n.slice,a=n.concat,s=n.push,u=n.indexOf,l={},c=l.toString,f=l.hasOwnProperty,p=f.toString,d=p.call(Object),h={},g=function e(t){return"function"==typeof t&&"number"!=typeof t.nodeType},y=function e(t){return null!=t&&t===t.window},v={type:!0,src:!0,noModule:!0};
```
Chúng ta có thể thấy với file Minified đã cắt bỏ các đoạn xuống dòng, các dấu cách không cần thiết và làm giảm dung lượng file một cách hiệu quả.
# 2.2 Obfuscated
Thông thường đối với các source public (Jquery, lodash, ...) thường thì sẽ chỉ có version minify để giảm dung lượng file khi load.

Đối với Obfuscated mặc dù cũng tương tự như Minified, nhưng nó còn làm thay đổi tên của các biến, hàm, ... làm cho chương trình khó hiểu hơn, và tiếp tục giảm kích thước file.

Việc này là cần thiết nếu các đoạn mã của bạn chứa các API, Key quan trọng và không muốn bị soi mói (yaoming)

Giả sử ta có đoạn code sau:
```
const getHuskyInu = () => {
 return 'N.B.L';
}

const getShinbaInu = () => {
  return 'D.A.D';
}
```
Với Obfuscated encode:
```
eval(function(p,a,c,k,e,d){e=function(c){return c};if(!''.replace(/^/,String))
{while(c--){d[c]=k[c]||c}k=[function(e){return d[e]}];e=function()
{return'\\w+'};c=1};while(c--){if(k[c]){p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c])}}return p}
('2 4=()=>{1\'3.5.6\'}2 8=()=>{1\'0.7.0\'}',9,9,'D|return|const|N|getHuskyInu|B|L|A|getShinbaInu'.split('|'),0,{}))
```

Với Obfuscated decode:
```
const getHuskyInu=()=>{return'N.B.L'}const getShinbaInu=()=>{return'D.A.D'}
```
# 2.3 Cách để Obfuscated code?

**Cách 1**. Thủ công mỹ nghệ tự viết lấy 1 thư viện (yaoming)

**Cách 2**. Xài các tool online như:

https://www.danstools.com/javascript-obfuscate/index.php

https://javascriptobfuscator.com/

https://javascriptobfuscator.com/Javascript-Obfuscator.aspx
