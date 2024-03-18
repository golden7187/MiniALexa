# MiniALexa
size = len(aggregated_df_yearly3.columns)

with pd.ExcelWriter('Split_Yearly_Summary.xlsx', engine='xlsxwriter') as writer:
    # Write Re_adjusted_contribution_new_yearlyI with heading and blue color
    k = 0
    for j in model_list:
        globals()[f'Re_adjusted_contribution_new_yearly{j}'].to_excel(writer, sheet_name='yearly summary', startrow=1, startcol=k*(size+2), index=True) 
        worksheet = writer.sheets['yearly summary']
        worksheet.write(1, k*(size+2), f'Yearly Aggregation of Model {j}', writer.book.add_format({'bold': True, 'font_color': 'black', 'bg_color': 'yellow', 'align': 'center', 'valign': 'vcenter', 'border': 1}))
        k += 1

    # Write aggregated_df_yearly3 with heading and blue color
    aggregated_df_yearly3.to_excel(writer, sheet_name='yearly summary', startrow=1, startcol=k*(size+2), index=True) 
    worksheet = writer.sheets['yearly summary']
    worksheet.write(1, k*(size+2), 'Yearly Agg of All Models', writer.book.add_format({'bold': True, 'font_color': 'black', 'bg_color': 'yellow', 'align': 'center', 'valign': 'vcenter', 'border': 1}))

    # Apply border to each cell in the table
    for i in range(size + 1):  # Including index column
        for j in range(len(model_list) + 1):  # Including header
            worksheet.set_row(j, None, writer.book.add_format({'border': 1}))
            worksheet.set_column(i, i, None, writer.book.add_format({'border': 1}))