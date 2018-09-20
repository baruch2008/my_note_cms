# my_note_cms
## 代建
1.终端菜单树同步
2.通用目录树规范制定

poi转excel，word文档为html
https://blog.csdn.net/u012954390/article/details/51325272

测试用页面
https://blog.csdn.net/wodewutai17quiet/article/details/53104034

@RequestMapping(value = "/importKPIExcelTable", method = RequestMethod.POST)
    public String importKPIExcelTable(HttpServletRequest request, HttpServletResponse response,
            @RequestParam(value = "targetFile", required = false) MultipartFile targetFile) throws Exception
    {
//        getTargetList(targetFile);
        HSSFWorkbook wb = new HSSFWorkbook(targetFile.getInputStream());
        String excelToHtml = excelToHtml(wb);
        System.out.println(excelToHtml);
        KPI kpi = new KPI();
        kpi.setKpiTableHtml(excelToHtml);
        kpiMapper.saveOrUpdateKPI(kpi);
//        // 设置response流信息的头类型，MIME码
//        response.setContentType("application/vnd.ms-excel;charset=UTF-8");
//        response.setHeader("Content-disposition", "attachment;filename=response.xls");
//        response.setCharacterEncoding("utf-8");
//        OutputStream ouputStream = response.getOutputStream();
//        // 将创建的Excel对象利用二进制流的形式强制输出到客户端去
//        wb.write(ouputStream);
//        // 强制将数据从内存中保存
//        ouputStream.flush();
//        ouputStream.close();
        return "success";
    }

## swagger的使用
### maven的配置
'''
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
</dependency>
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
</dependency>
'''
### restful注解的使用
@ApiOperation(value notes) --接口本身的说明notes起说明作用
@ApiResponses({@ApiResponse(code message response)}) --响应体的简单说明message起说明作用
@ApiImplicitParams({@ApiImplicitParam(name value)}) --请求体与请求参数的简单说明name对应@RequestParam中的value，value起说明作用

## Mybatis 标签使用
### '<choose><when><otherwise>'
等价于sql语句中的
    1. if(exp1,true_result,false_result)
    2. case when exp1 then true_result
        else 1=1 end
    
    
public ResponseResult<String> importKPIExcelTable(
            @RequestParam(value = "targetFile", required = false) MultipartFile targetFile) throws Exception
    {
    }
     String excelToHtml = null;
        // excel转换为html
        Workbook wb = WorkbookFactory.create(targetFile.getInputStream());
        if (wb instanceof XSSFWorkbook)
        {
            XSSFWorkbook xWb = (XSSFWorkbook) wb;
            excelToHtml = xlsxToHtml(xWb);
        }
        else if (wb instanceof HSSFWorkbook)
        {
            HSSFWorkbook hWb = (HSSFWorkbook) wb;
            excelToHtml = PoiUtil.excelToHtml(hWb);
        }
    public static String excelToHtml(HSSFWorkbook excelBook) throws Exception
    {

        ExcelToHtmlConverter ethc = new ExcelToHtmlConverter(DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument());
        ethc.setOutputColumnHeaders(false);
        ethc.setOutputRowNumbers(false);

        ethc.processWorkbook(excelBook);

        Document htmlDocument = ethc.getDocument();
        ByteArrayOutputStream out = new ByteArrayOutputStream();
        DOMSource domSource = new DOMSource(htmlDocument);
        StreamResult streamResult = new StreamResult(out);

        TransformerFactory tf = TransformerFactory.newInstance();
        Transformer serializer = tf.newTransformer();
        serializer.setOutputProperty(OutputKeys.ENCODING, "UTF-8");
        serializer.setOutputProperty(OutputKeys.INDENT, "yes");
        serializer.setOutputProperty(OutputKeys.METHOD, "html");
        serializer.transform(domSource, streamResult);
        out.close();

        String htmlStr = new String(out.toByteArray());

        // htmlStr = htmlStr.replace("<h2>Sheet1</h2>", "")
        // .replace("<h2>Sheet2</h2>", "")
        // .replace("<h2>Sheet3</h2>", "")
        // .replace("<h2>Sheet4</h2>", "")
        // .replace("<h2>Sheet5</h2>", "");
        htmlStr = htmlStr.replace("<h2>Sheet1</h2>", "");
        return htmlStr;
    }
    java xlsx转html
   http://bewithme.iteye.com/blog/2418535
   支持07 03excel转html可用demo
   https://www.cnblogs.com/linshangxixia/p/4442665.html
   获取<style> <table>标签
 String regEx_style = "<[\\s]*?style[^>]*?>[\\s\\S]*?<[\\s]*?\\/[\\s]*?style[\\s]*?>";
        String regEx_table = "<[\\s]*?table[^>]*?>[\\s\\S]*?<[\\s]*?\\/[\\s]*?table[\\s]*?>";

构件支持全文检索的日志服务
drwxr-xr-x  9 elkuser elkgroup  145 Sep 17 09:47 elasticsearch-5.2.0/
drwxrwxr-x 12 elkuser elkgroup 4096 Sep 17 11:07 kibana-5.2.0-linux-x86_64/
drwxr-xr-x 12 root    root     4096 Sep 17 09:48 logstash-5.2.0/
