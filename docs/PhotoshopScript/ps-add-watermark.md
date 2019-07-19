# [脚本]批量添加水印
```javascript
/*
// author: wuguanlin
// Open a given folder and compress all JPEG images with Tinify.
// Copyright (c) 2015 Voormedia B.V. All rights reserved.

<javascriptresource>
<menu>automate</menu>
<category>LinDevelop</category>
<name>$$$/LinDevelopFolder2/Menu=[lin]批量加水印</name>
<eventid>808034C2-162D-481B-88D4-B3EF294EDE42</eventid>
</javascriptresource>

*/

/**
 * 批量加水印
 */

(function() {
  app.preferences.rulerUnits = Units.PIXELS;

  var watermarkPos = null; // 水印位置，相对文档右上角
  var watermarkFile = File.openDialog("FILE 请选择印在图片上的文件");
  var inputFolder = Folder.selectDialog("INPUT 选择被加水印的图片的文件夹");
  var outputFolder = Folder.selectDialog("OUTPUT 选择输出文件夹");

  if (!watermarkFile || !inputFolder || !outputFolder) {
    return;
  }
  /**
   * 记录
   */
  var wrongTips = ""; // 记录失败的图片名字和错误原因
  var successNumber = 0; // 记录成功的图片数
  var failNumber = 0; // 记录失败的图片数

  /**
   * 复制水印
   */
  var watermarkFileRef = new File(watermarkfile.fullName); // 创建水印文件
  var watermarkFileDocumentRef = app.open(watermarkFileRef); // 新建文档
  // var watermarkFileObj = {
  //   width: watermarkFileDocumentRef.width,
  //   height: watermarkFileDocumentRef.height
  // }
  watermarkFileDocumentRef.artLayers[0].copy(); // 复制水印文件
  watermarkFileDocumentRef.close(); // 关闭水印文档

  /**
   * 设置导出类型
   */
  var pngExportOptions = new ExportOptionsSaveForWeb();
  pngExportOptions.format = SaveDocumentType.PNG;
  pngExportOptions.PNG8 = false;
  pngExportOptions.transparency = true;

  var jpgExportOptions = new ExportOptionsSaveForWeb();
  jpgExportOptions.format = SaveDocumentType.JPEG;
  jpgExportOptions.quality = 60;

  /**
   * 设置水印的位置，相对文档右上角偏移
   */
  if (
    confirm(
      "温馨提示：\n是否需要设置水印的位置（默认添加在文档中间）（单位px）？"
    )
  ) {
    watermarkPos = {
      x: 0,
      y: 0
    };
    watermarkPos.x = prompt("请设置水印的X坐标", 0);
    watermarkPos.y = prompt("请设置水印的Y坐标", 0);
    !/^[0-9]*$/.test(watermarkPos.x) && (watermarkPos.x = 0); // 容错
    !/^[0-9]*$/.test(watermarkPos.y) && (watermarkPos.y = 0); // 容错
  }
  var watermarkOpacity = prompt("请设置水印的透明度(0-100)", 100);

  !/^[0-9]*$/.test(watermarkOpacity) && (watermarkOpacity = 100); // 容错

  /**
   * 批量添加水印
   */
  var children = inputFolder.getFiles();

  for (var i = 0; i < children.length; i++) {
    var child = children[i];
    if (child instanceof Folder) {
    } else {
      try {
        curFileName = child.name; // 记录当前处理的图片名称
        if (
          child.name.slice(-5).toLowerCase() == ".jpeg" ||
          child.name.slice(-4).toLowerCase() == ".jpg" ||
          child.name.slice(-4).toLowerCase() == ".png"
        ) {
          pictureRef = new File(child.fullName); // 创建文件
          pictureDocumentRef = app.open(pictureRef); // 新建文档
          pictureDocumentRef.paste(); // 黏贴

          watermarkOpacity !== null &&
            (pictureDocumentRef.activeLayer.opacity = watermarkOpacity); // 设置透明度
          /**
           * 如果设置了水印的位置
           */
          if (watermarkPos) {
            pictureDocumentRef.activeLayer.translate(
              -pictureDocumentRef.activeLayer.bounds[0],
              -pictureDocumentRef.activeLayer.bounds[1]
            ); // 移动到0，0 位置
            pictureDocumentRef.activeLayer.translate(+watermarkPos.x, +watermarkPos.y); // 移动位置
          }

          pictureDocumentRef.exportDocument(
            new File(outputFolder + "/" + curFileName),
            ExportType.SAVEFORWEB,
            child.name.slice(-4).toLowerCase() == ".png"
              ? pngExportOptions
              : jpgExportOptions
          ); // 导出图片到输出目录
          pictureDocumentRef.close(SaveOptions.DONOTSAVECHANGES); // 关闭当前文档
          successNumber++;
        }
      } catch (error) {
        failNumber++;
        wrongTips += "\n" + curFileName + "    " + error;
      }
    }
  }

  var tips = "files add end.";
  if (failNumber > 0) {
    tips = "JPEG和PNG图片修改完毕！但是" + failNumber + "个文件修改失败：";
    tips += wrongTips;
  } else {
    tips =
      "恭喜您，所有JPEG和PNG图片都修改完毕！（" + successNumber + "个文件）";
  }
  alert(tips);

  /**
   * 关闭所有文档
   */
  function closeAllDoc() {
    while (app.documents.length) {
      app.activeDocument.close();
    }
  }
})();

```