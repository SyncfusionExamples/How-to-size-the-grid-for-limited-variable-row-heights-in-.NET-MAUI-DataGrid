# How to size the grid for limited variable row heights in .NET MAUI DataGrid
This demo shows how to size the Syncfusion .NET MAUI SfDataGrid to display a limited number of rows when rows have variable heights. By using this sample, you can preserve per-row height differences, show only a specified number of rows (for example, the first five) and still allow the user to scroll for any remaining rows.

You compute the combined height of the header row plus the first N data rows and set the DataGrid’s `HeightRequest` during the grid’s Loaded event. Ensure `MinimumHeightRequest` is set to 0 so the grid can shrink as needed. Use Math.Min to avoid reading beyond the available records, and call `GetRowHeight` for each row to respect individual row heights. With this approach, the grid displays the exact number of rows you want while keeping correct variable row sizing and scrollability for additional data.

```
private void dataGrid_Loaded(object sender, EventArgs e) 
{
        dataGrid.MinimumHeightRequest = 0;
        double totalHeight = dataGrid.HeaderRowHeight;
        var view = dataGrid.View; 
        for (int i = 0; i < Math.Min(5, view.Records.Count); i++)
        {
            totalHeight += dataGrid.GetRowHeight(i, false);
        } 
        dataGrid.HeightRequest = totalHeight;
}
```
