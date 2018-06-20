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
### <choose><when><otherwise>
等价于java中的
    if(){}
    else if(){}
    else{}
