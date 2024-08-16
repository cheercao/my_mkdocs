# Report

`Report` 类是一个用于生成和操作 Word 文档的实用工具。通过该类，用户可以轻松创建专业化的报告文档。`Report` 类不仅能够插入和定制标题、段落、图片和表格等内容，还支持对文档中字体、对齐方式、单元格边框等元素进行详细设置。借助这些功能，用户能够生成具有统一格式和美观排版的文档，适用于各类报告生成需求。

### Report(cover_path)

初始化 `Report` 类后，可以选择性地指定报告的封面路径。如果没有指定封面路径，系统将生成一个默认的空白文档作为报告的起始页。

> 参数：

- **`cover_path`** (str): 报告封面路径。

> **使用示例**

```python
report = Report('wtai_dt/SampleData/report_data/封面.docx')
```

> report.create_new_document()

`create_new_document` 函数用于创建一个新的Word文档。如果在初始化报告类时指定了封面路径，那么该函数会基于指定的封面路径创建一个新的Word文档；如果没有指定封面路径，则会创建一个默认的空白Word文档。这个函数可以确保生成的文档符合报告的特定需求，无论是有封面还是无封面的情况。

> **参数**

> **使用示例**

```python
world = report.create_new_document()
```

### report.insert_title(doc, title_text)

`insert_title` 函数用于在Word文档中插入一级标题。调用该函数时，用户需要提供文档对象和标题文本。函数将自动将标题文本设置为加粗、黑色的宋体，并使用一级标题样式（`level=1`）和12磅字体大小，从而保证文档中标题的一致性和规范性。通过此函数，用户可以轻松创建格式统一的章节标题。

> **参数**

- **`doc`** (Document): 写入内容的报告类。
- **`title_text** (str): 写入报告文档的一级标题内容。

> **使用示例**

```python
big_title = 1
report.insert_title(world, str(big_title) + "、 " + "机组发电性能分析")
```

### report.insert_lettle_title_word(doc, lettle_text)

`insert_lettle_title_word` 函数用于在Word文档中插入二级标题，并自定义标题的格式。该函数通过调用 `doc.add_heading(level=2)` 创建一个二级标题，并设置标题的字体为宋体、加粗、黑色，字号为12磅。此外，还为标题指定了适合中文的字体配置，确保标题在中英文混排时的显示效果。这个函数适合用于插入具有强调作用的小标题，使文档结构更加清晰。

> **参数**

- **`doc`** (Document): 写入内容的报告类。
- **`lettle_text`** (str): 写入报告文档的二级标题内容。

> **使用示例**

```python
small_title = 1
report.insert_lettle_title_word(world,str(big_title) + '.' + str(small_title) + "、 各风机风速和电量分析结果")
```

### report.insert_image_table(doc, image_paths, image_name, num_cols_per_table=2)

`insert_image_table` 函数用于在 Word 文档中插入一个包含图像的表格。用户可以指定图像的路径、图像的名称，以及每个表格中包含的列数。函数将根据提供的图像数量自动创建多个表格，并将每张图像及其对应的名称插入到表格的单元格中。每个图像会自动调整为适合单元格的宽度，并且表格的边框将被移除，使得整个图表布局更加美观、整齐。此函数适用于需要批量插入和展示多个图像的场景。

> **参数**

- **`doc`** (Document): 写入内容的报告类。
- **`image_paths`** (list): 存储图片表格的图片路径。
- **`image_name`** (list): 存储与图片路径一一对应的图片标题。
- **`num_cols_per_table`** (int): 设置表格的列数。

> **使用示例**

```python
name = ['风机 28', '风机 29', '风机 30']
path = ['C:/Users/86152/Desktop/风机28 风速-功率曲线.png', 'C:/Users/86152/Desktop/风机29 风速-功率曲线.png', 'C:/Users/86152/Desktop/风机30 风速-功率曲线.png']
for id, content in save_type.items():
    if content['type'] == 'image':
        name.append(id)
        path.append(utility.resource_path(content['data'][0]).replace('\\', '/').replace('./', ''))
        report_content = report_content + content['content']
report.insert_image_table(world, path, name)
```

### report.insert_paragraph(doc, text, font_name=u'宋体', font_size=12)

`insert_paragraph` 函数用于在 Word 文档中插入一段新的文本段落。用户可以指定文本内容、字体名称和字体大小。该函数会自动在段落前添加缩进，并对段落中的每个文本运行（run）应用指定的字体和大小格式。通过这种方式，可以确保文档中的段落格式一致，适用于需要插入描述性文本或解释内容的场景。

> **参数**

- **`doc`** (Document): 写入内容的报告类。
- **`text`** (str): 写入报告的文本段落内容。
- **`font_name`** (str): 文本段落字体。
- **`font_size`** (str): 文本段落字号。

> **使用示例**

```python
report.insert_paragraph(world, report_content)
```

### report.insert_table_word(doc, data)

`insert_table_word` 函数用于在 Word 文档中插入一个表格，并根据提供的数据自动填充表格的内容。函数会首先创建一个包含标题行的表格，然后逐行添加数据，确保每个单元格的文本格式统一（如字体、颜色和大小）。此外，该函数还会设置单元格的对齐方式，使表格内容在视觉上更加整齐和专业。此功能适用于需要在报告中展示结构化数据或统计信息的场景。。

> **参数**

- **`doc`** (Document): 写入内容的报告类。
- **`data`** (list): 写入报告的表格数据。

> **使用示例**

```python
data = [['风机', '平均风速(m/s)', '年平均风速(m/s)', '理论电量(kw·h)', '实际电量(kw·h)', '数据开始时间', '数据结束时间'], ['28', '6.996', "{'2024年风速': '6.996'}", '1033793', '805080', '2024-04-01 00:00:00', '2024-06-01 23:59:59'], ['29', '6.156', "{'2024年风速': '6.156'}", '503275', '783300', '2024-04-01 00:00:00', '2024-06-01 23:59:59'], ['30', '7.781', "{'2024年风速': '7.781'}", '1050575', '776880', '2024-04-01 00:00:00', '2024-06-01 23:59:59']]
report.insert_table_word(world, final_list)
```

