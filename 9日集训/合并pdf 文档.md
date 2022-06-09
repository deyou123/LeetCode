# 如何合并pdf 文档
```java
<dependencies>
    <dependency>
        <groupId>com.itextpdf</groupId>
        <artifactId>itext7-core</artifactId>
        <version>7.1.16</version>
        <type>pom</type>
    </dependency>
</dependencies>
```



java 代码

```java
import com.itextpdf.kernel.pdf.PdfDocument;
import com.itextpdf.kernel.pdf.PdfReader;
import com.itextpdf.kernel.pdf.PdfWriter;
import com.itextpdf.kernel.utils.PdfMerger;

import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.util.UUID;
public class CE06E04Combine {
    private static final String FILE_NAME1 = "";
    private static final String FILE_NAME2 = "";
    private static final String DEST = "";

    public static void main(String[] args) throws Exception {
        CE06E04Combine ce06E04Combine = new CE06E04Combine();
        ce06E04Combine.combinePDF(FILE_NAME1, FILE_NAME2,DEST);
        //ce06E04Combine.combinePDF(FILE_NAME1, FILE_NAME2);
        //存放文件目录
        //String path = "";
        //ce06E04Combine.combinePDF2( path,path );
    }

    /**
     * 合并2个文档
     * @param fileName1
     * @param fileName2
     * @return
     */
    private void combinePDF(String fileName1,String fileName2){
        String desFileName = new File(fileName1).getParentFile().getAbsolutePath()+"/" + UUID.randomUUID()+".pdf";
        combinePDF(fileName1,fileName2,desFileName);
    }
    private void combinePDF(String fileName1, String fileName2, String desFileName)  {
        PdfDocument pdf = null;
        try {
            pdf = new PdfDocument(new PdfWriter(desFileName));
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        //定义合并文档
        PdfMerger merger = new PdfMerger(pdf);
        //添加第一个文档
        PdfDocument firstSourcePdf = null;
        try {
            firstSourcePdf = new PdfDocument(new PdfReader(fileName1));
        } catch (IOException e) {
            e.printStackTrace();
        }
        merger.merge(firstSourcePdf, 1, firstSourcePdf.getNumberOfPages());
        //添加第二个文档
        PdfDocument secondSourcePdf = null;
        try {
            secondSourcePdf = new PdfDocument(new PdfReader(fileName2));
        } catch (IOException e) {
            e.printStackTrace();
        }

        merger.merge(secondSourcePdf, 1, secondSourcePdf.getNumberOfPages());

        // 合并并关闭
        merger.close();
        firstSourcePdf.close();
        secondSourcePdf.close();
        pdf.close();
    }

    /**
     * 合并文件夹下多个pdf 文档
     * @param parentDir 目标路径
     * @param desPath  //合并后文档输出地址
     */
    private void combinePDF2(String parentDir, String desPath)  {

        String[] files = new File(parentDir).list();

        String desFileName = desPath  +UUID.randomUUID().toString()+".pdf";
        PdfDocument pdf = null;
        try {

            pdf = new PdfDocument(new PdfWriter(desFileName));

        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
        //定义合并文档
        PdfMerger merger = new PdfMerger(pdf);

        //添加第一个文档
        PdfDocument sourcePdf = null;
        for (String file : files) {
            String file1 = parentDir+file;
            try {
                sourcePdf = new PdfDocument(new PdfReader(file1));
            } catch (IOException e) {
                e.printStackTrace();
            }
            merger.merge(sourcePdf, 1, sourcePdf.getNumberOfPages());
        }

        // 合并并关闭
        merger.close();
        sourcePdf.close();
        pdf.close();
    }
}

```

