utilisation dans export des tables statistiques dans sesa stat
```js
<!-- use version 0.19.3 -->
<
script lang = "javascript"
src = "https://cdn.sheetjs.com/xlsx-0.19.3/package/dist/xlsx.full.min.js" > < /script> <
    script >

    //export sur plusiers sheets 
    // document.getElementById("btnPrint").addEventListener('click', function() {

    //   //creation d'un workbook 
    //   var workbook = XLSX.utils.book_new();

    //   /* Create worksheet from HTML DOM TABLE */
    //   var ws1 = XLSX.utils.table_to_sheet(document.getElementById("data"));
    //   var ws2 = XLSX.utils.table_to_sheet(document.getElementById("data2"));

    //   XLSX.utils.book_append_sheet(workbook,ws1,"Sheets1");
    //   XLSX.utils.book_append_sheet(workbook,ws2,"Sheets2");
    //   /* Export to file (start a download) */
    //   XLSX.writeFile(workbook, "SheetJSTable.xlsx");
    // });

    //export de plusieurs tables sur un sheet 
    document.getElementById("btnPrint").addEventListener('click', function() {
        let tbl1 = document.getElementById("data")
        let tbl2 = document.getElementById("data2")

        let worksheet_tmp1 = XLSX.utils.table_to_sheet(tbl1);
        let worksheet_tmp2 = XLSX.utils.table_to_sheet(tbl2);

        let a = XLSX.utils.sheet_to_json(worksheet_tmp1, {
            header: 1
        })
        let b = XLSX.utils.sheet_to_json(worksheet_tmp2, {
            header: 1
        })

        a = a.concat(['']).concat(b)

        let worksheet = XLSX.utils.json_to_sheet(a, {
            skipHeader: true
        })

        const new_workbook = XLSX.utils.book_new()
        XLSX.utils.book_append_sheet(new_workbook, worksheet, "worksheet")
        XLSX.writeFile(new_workbook, 'tmp_file.xls')
    });
<
/script>
```