---
title: Using XlsxFormatProvider
page_title: Using XlsxFormatProvider
description: Using XlsxFormatProvider
slug: radspreadprocessing-formats-and-conversion-xlsx-xlsxformatprovider
tags: using,xlsxformatprovider
published: True
position: 2
---

# Using XlsxFormatProvider



__XlsxFormatProvider__ makes it easy to import and export xlsx files. An xlsx file is a group of zipped files that conform to the Office Open XML schema. That said, the format allows you export all parts of a workbook: worksheets, formula values, formatting, hyperlinks, etc.
      

>Unlike the csv and txt format providers, the __XlsxFormatProvider__ requires references to the following assemblies:
        

>* Telerik.Windows.Documents.Spreadsheet.FormatProviders.OpenXml.dll
            

>* Telerik.Windows.Zip.dll
            

Once you reference the aforementioned assemblies, you need to create an instance of the __XlsxFormatProvider__ in order to import and export xlsx files. This provider appears in the Telerik.Windows.Documents.Spreadsheet.FormatProviders.OpenXml.Xlsx namespace. __XlsxFormatProvider__ implements the __IWorkbookFormatProvider__ interface, which in turn appears in the Telerik.Windows.Documents.Spreadsheet.FormatProviders. Depending on the whether you would like to work with the concrete class or the interface, you would need to include either the first or both namespaces.
      

## Import

__Example 1__ shows how to import an xlsx file using a FileStream. The code assures that a file with the specified name exists. Further, the sample instantiates an __XlsxFormatProvider__ and passes a FileStream to its __Import()__ method.
        

#### __[C#] Example 1: Import Xlsx file__

{{region cs-radspreadprocessing-formats-and-conversion-xlsx-xlsxformatprovider_0}}
	string fileName = "SampleFile.xlsx";
	if (!File.Exists(fileName))
	{
	    throw new FileNotFoundException(String.Format("File {0} was not found!", fileName));
	}
	
	Telerik.Windows.Documents.Spreadsheet.Model.Workbook workbook;
	IWorkbookFormatProvider formatProvider = new Telerik.Windows.Documents.Spreadsheet.FormatProviders.OpenXml.Xlsx.XlsxFormatProvider();
	
	using (Stream input = new FileStream(fileName, FileMode.Open))
	{
	    workbook = formatProvider.Import(input);
	}
{{endregion}}



## Export

__Example 2__ demonstrates how to export an existing Workbook to an xlsx file. The snippet creates a new workbook with a single worksheet. Further, the example creates an __XlsxFormatProvider__ and invokes its __Export()__ method. Note that the __Export()__ method accepts a parameter of type __Stream__ so you can work with any of its inheritors.
        

#### __[C#] Example 2: Export Xlsx file__

{{region cs-radspreadprocessing-formats-and-conversion-xlsx-xlsxformatprovider_1}}
	Telerik.Windows.Documents.Spreadsheet.Model.Workbook workbook = new Telerik.Windows.Documents.Spreadsheet.Model.Workbook();
	workbook.Worksheets.Add();
	string fileName = "SampleFile.xlsx";
	
	IWorkbookFormatProvider formatProvider = new Telerik.Windows.Documents.Spreadsheet.FormatProviders.OpenXml.Xlsx.XlsxFormatProvider();
	
	using (Stream output = new FileStream(fileName, FileMode.Create))
	{
	    formatProvider.Export(workbook, output);
	}
{{endregion}}


