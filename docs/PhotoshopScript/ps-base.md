# PhotoshopScript 基础

## 脚本位置
Mac: /Applications/Adobe Photoshop (version)/Presets/Scripts/
Windows: C:\Program Files\Adobe\Adobe Photoshop (version)\Presets\Scripts\

可以在 ‘文件’-‘自动’ 找到载入的脚本

## 文件
```javascript
// 选择单个文件
var file = File.openDialog("FILE 请选择印在图片上的文件");
// 选择文件夹
Folder.selectDialog("INPUT 选择被加水印的图片的文件夹");
// 读取文件
new File(file.fullName); // 创建水印文件
```

## 确定操作
```javascript
if (confirm("温馨提示：\n您将要压缩所选文件夹和所有子文件夹中的所有JPEG和PNG文件，这不能被撤消。\n\r您确定您要继续吗？")) {
}
```

## 文本输入
```javascript
var value = prompt("Type in the name of the file", "filename.png")
```

## 文档

### 新建文档
```javascript
// 方法1
var fileRef = new File(file.fullName); // 创建水印文件
var fileDocumentRef = app.open(fileRef); // 新建文档

// 方法2
//定义一个变量[Width]，表示新文档的宽度。
var width = 560;
//定义一个变量[height]，表示新文档的高度。
var height = 560;
//定义一个变量[resolution]，表示新文档的分辨率。
var resolution = 72;
//定义一个变量[docName]，表示新文档的名称。
var docName = "New Document";
//定义一个变量[mode]，表示新文档的颜色模式。
var mode = NewDocumentMode.RGB;
//定义一个变量[initialFill]，表示新文档的默认背景填充颜色。
var initialFill = DocumentFill.TRANSPARENT;
//定义一个变量[pixelAspectRatio]，用来设置新文档的像素比率。
var pixelAspectRatio = 1;
app.documents.add(width, height, resolution, docName, mode, initialFill, pixelAspectRatio);
```

### 导出文档
```javascript
var document = app.activeDocument;
//定义一个变量[fileOut]，用来表示导出后的图片路径。
var fileOut = new File('C:\\compressed.jpeg');
//定义一个变量[exportOptionsSaveForWeb]，用来表示导出文档为Web格式的设置属性。
var exportOptionsSaveForWeb = new ExportOptionsSaveForWeb();
//设置导出文档时，图片将被存储为.jpeg格式。
exportOptionsSaveForWeb.format = SaveDocumentType.JPEG;
//设置导出文档时，图片的压缩质量。数字范围为1至100。
exportOptionsSaveForWeb.quality = 60;
// 导出图片到输出目录
document.exportDocument(new File(fileOut), ExportType.SAVEFORWEB, jpgExportOptions);
```

### 关闭文档
```javascript
var document = app.activeDocument;
document.close(SaveOptions.DONOTSAVECHANGES); // 关闭当前文档
```

## 图层

### 当前图层
```javascript
app.activeDocument.activeLayer
```

### 移动
```javascript
app.activeDocument.activeLayer.translate(0, -200); // 移动位置
```
