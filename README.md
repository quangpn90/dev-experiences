THANK TO [REACT-BOILERPLATE](https://github.com/react-boilerplate/react-boilerplate)

- Với mục đích ghi chép kinh nghiệm trong quá trình làm việc để lưu trữ
cho các bạn tìm hiểu sau này cũng như phục vụ công việc mentor của bản thân sau này!
- Bài viết hoàn toàn từ kinh nghiệm nên sẽ không phải là bài viết lý thuyết xuông
mà còn đưa ra ví dụ cụ thể.

Các bài viết về React
- Tại sao không nên sử dụng jQuery trong React: https://github.com/nguyenvanhoang26041994/dev-experiences/tree/why-should-not-use-jquery-with-react
- Vòng đợi/life cycle của React Compoennt: https://github.com/nguyenvanhoang26041994/dev-experiences/blob/master/React/lifecycle_hook.md
- Tất tật tật các cách tối đa performace cho ứng dụg React: https://github.com/nguyenvanhoang26041994/dev-experiences/blob/master/React/how_to_make_best_performance.md
- Những loại component trong React và cách sử dụng đúng: https://github.com/nguyenvanhoang26041994/dev-experiences/blob/master/React/how_many_component_types.md
- PureComponent vs Component: https://github.com/nguyenvanhoang26041994/dev-experiences/blob/master/React/component_vs_purecomponent.md
 
#-------Dưới đây chỉ là nháp cá nhân thôi, các bạn không cần phải quan tâm---
https://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories-on-rebase
https://stackoverflow.com/questions/10697463/resolve-git-merge-conflicts-in-favor-of-their-changes-during-a-pull
https://stackoverflow.com/questions/32370994/how-to-pass-props-to-this-props-children
https://devhints.io/sass
Draff:
- Check eslint trước khi commit
  pre-commit
  husky
  lint-staged
- Client HTML to PDF: https://github.com/MrRio/jsPDF
  live demo: https://rawgit.com/MrRio/jsPDF/master/#
- Client export excel: https://github.com/SheetJS/js-xlsx

- Tìm kiếm HTML symbold: http://graphemica.com/search?page=5&q=down
- https://github.com/akiran/react-slick
- Coding standar: http://airbnb.io/javascript/
- Ở webpack 4 không thể parse file json bình thường như webpack 3 vẫn làm được. Nên phải config lại một chút như này:
```javascript
{
  test: /\.json/,
  type: 'javascript/auto',
  exclude: /node_modules|bower_components/,
  use: [require.resolve('json-loader')],
},
```

- https://github.com/ckeditor/ckeditor5
- https://www.pdfonline.com/convert-pdf-to-html/
- https://templates.mailchimp.com/resources/inline-css/
- https://babeljs.io/blog/2018/08/27/7.0.0
 
babel 7 có nhiều thứ hay ho như <></> render React.Fragment, suport TS. 
- babel-plugin-proposal-optional-chaining cái này siêu hay, trước phải a && a.b && a.b.c thì bây giờ chỉ cần a?.b?.c thôi hoặc onHandle && onHandle() thì chỉ cần onHandle?.()
- babel-plugin-proposal-logical-assignment-operators cũng khá ngầu nhưng chắc ít dùng
 trước: a = a || b, thì bây giơ sẽ chỉ cần a ||= b, tương tự, a = a && b thì chỉ cần a &&= b;, khá cool.
- @babel/preset-typescript cái này setting thương tự @babel/preset-flow, vậy là từ đây, React ngày càng flexible
- <></> ????.

 
Với template, Ví dụ:
chuỗi string `<div>Tôi là {{ name }}</div>` thì có thể sử dụng nhiều template hbs.
- npm i handlebars
```javascript
import Handlebars from 'handlebars';

export const fillVariables = (template, variables) => Handlebars.compile(template)(variables);

```
- config webpack.
```javascript
{
...
  node: {
    fs: 'empty'
  }
...
}
```
- Clourse + React
- http://www.boilrplate.com/
- https://github.com/MrRio/jsPDF/blob/master/examples/html2pdf/
- https://stackoverflow.com/questions/44613818/how-to-send-by-ajax-a-pdf-file-autogenerated
- https://bundlephobia.com/
- https://thachpham.com/web-development/html-css/11-bo-suu-tap-hieu-ung-css3-dep.html
- https://codepen.io/zadvorsky/pen/PNXbGo


# html2pdf
```javascript
export const dataURItoBlob = dataURI => {
  // convert base64/URLEncoded data component to raw binary data held in a string
  let byteString;
  if (dataURI.split(',')[0].indexOf('base64') >= 0) {
    byteString = atob(dataURI.split(',')[1]);
  } else {
    byteString = unescape(dataURI.split(',')[1]);
  } 

  // separate out the mime component
  const mimeString = dataURI.split(',')[0].split(':')[1].split(';')[0];

  // write the bytes of the string to a typed array
  const ia = new Uint8Array(byteString.length);
  for (var i = 0; i < byteString.length; i++) {
    ia[i] = byteString.charCodeAt(i);
  }

  return new Blob([ia], { type: mimeString });
};

export const createPDFFile = (dataURI, filename) =>
  new File([dataURItoBlob(dataURI)], filename, { type: 'application/pdf' }); 
```
```javascript
import html2PDF from 'html2pdf.js';
import Handlebars from 'handlebars';
import { createPDFFile } from './create-pdf-file';

export const fillVariables = (template, variables) => Handlebars.compile(template)(variables);

export const renderPDFWithDownload = (template, filename, variables) => {
  html2PDF()
    .from(fillVariables(template, variables))
    .toPdf()
    .save(filename);
};

export const renderPDFWithCallback = (template, filename, variables, callback) => {
  html2PDF()
    .from(fillVariables(template, variables))
    .toPdf()
    .output('datauristring')
    .then(blobData => callback(createPDFFile(blobData, `${filename}.pdf`)));
};

```
```javascript
import InlineEditor from '@ckeditor/ckeditor5-build-inline';

InlineEditor
    .create(document.querySelector('.ck-editor'), { toolbar: ['heading', '|', 'bold', 'italic', 'link']})
    .then(editor => window.editor = editor);
```

__________
1. Plugin hover css (Tạo hiệu ứng khi rê chuột - vào) :
http://ianlunn.github.io/Hover/
2. Plugin Animate.css (Tổng hợp 1 số animate css, cũng là hiệu ứng):
- https://daneden.github.io/animate.css/
3.Plugin Image hover (Tạo hiệu ứng khi rê chuột vào ảnh) :
- http://imagehover.io/
4. Owl carousel (Slider cho website) :
- https://owlcarousel2.github.io/OwlCarousel2/
5. Slick slider (Slider cho website - nhẹ hơn owl carousel, bác nào thích hiệu ứng có thể dùng owl carousel, thích đơn giản thì dùng thằng này) :
- http://kenwheeler.github.io/slick/
Bác nào muốn hiệu ứng cho slick slider có thể dùng thêm thằng bên dưới
- https://github.com/marvinhuebner/slick-animation (Hỗ trợ hiệu ứng cho slick slider, cần có animate.css)
6. Plugin Wow js (Tạo hiệu ứng xuất hiện khi cuộn trang) :
- https://wowjs.uk/
7. Plugin Isotope (Tạo hiệu ứng mỗi khi click vào filter) :
- https://isotope.metafizzy.co/
8. Direction Reveal (Tạo hiệu ứng khi rê chuột vào sẽ theo hướng di chuyển của chuột - xem demo để rõ hơn) :
- https://nigelotoole.github.io/direction-reveal/
9. Plugin Scroll With Ease (Tạo hiệu ưng ease khi lăn chuột) :
- https://www.jqueryscript.net/…/Configurable-Smooth-Scrollin…
10. Font Awesome Animation (Hiệu ứng cho Font Awesome):
- http://l-lin.github.io/font-awesome-animation/
11. Framework Material Design for Bootstrap (Bản custom bootstrap với material design) :
- https://fezvrasta.github.io/bootstrap-material-design/
12. Materialize (Framework với phong cách material design) :
- https://materializecss.com/
13. Plugin ScrollReveal (Tạo hiệu ưng xuất hiện khi cuộn trang giống Wow js nhưng cái này có độ delay từng phần tử ):
- https://scrollrevealjs.org/
14. Keyframes (Tạo animation có bản web và bản extension chrome) :
- https://keyframes.app/
15. Plugin Tilt (Tạo hiệu ứng parallax khi rê chuột vào phần tử) :
- https://gijsroge.github.io/tilt.js/
16. Plugin Particles (Tạo hiệu ứng ngân hà Một số plugin front end chủ yếu thiên về UI:v theo em thì là vậy) :
- https://vincentgarreau.com/particles.js/
17. Plugin LegitRipple (Tạo hiệu ứng ripple wave khi click vào phần tử) :
- https://matthias-vogt.github.io/legitRipple.js/
18. Plugin Splitting (Tạo hiệu ứng text, image, list.... cho website) :
- https://splitting.js.org/
19. Plugin Fancybox (Tạo hiệu ứng khi xem ảnh) :
- https://www.fancyapps.com/fancybox/3/
20. Plugin Anime JS (Tạo hiệu ứng cho phần tử) :
- http://animejs.com/

http://cssnext.io/features/
_______________________________________________
Install `nvm` in macOS
https://www.codementor.io/mercurial/how-to-install-node-js-on-macos-sierra-mphz41ekk
