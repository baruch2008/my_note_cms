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
