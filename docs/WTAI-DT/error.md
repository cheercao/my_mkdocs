# SCADAError

`SCADAError` 类用于处理和分析SCADA系统中的故障数据。它的构造函数接收故障数据、风机字段、故障开始和结束时间字段、故障类型字段以及故障分析方法（如故障次数和停机时间）作为参数。这些参数用于初始化类实例，以便对故障进行系统化分析。

### SCADAError(data, wind_field,start_time_field,end_time_field,error_type_field,function)

初始化 SCADA 故障分析类后，该类可以分析 SCADA 数据中的故障时间、故障次数，并对故障进行详细分类统计。具体的故障类别包括变流器故障、变桨故障、偏航故障、主控故障、发电机故障、润滑故障、水冷故障以及其他故障。这种分类和分析有助于全面了解和管理风机的运行状态及维护需求。

> 参数：

- **`data`** (DataFrame): 故障数据。
- **`wind_field`** (str): 风机字段。
- **`start_time_field`** (str): 故障开始时间字段。
- **`end_time_field`** (str): 故障结束时间字段。
- **`error_type_field`** (str): 故障类型字段。
- **`function`** (Callable): 故障分析方法，接受的功能包括故障次数、停机时间等。

> **使用示例**

```python
data = pd.read_csv('wtai_dt/SampleData/SCADA_Error/SampleErrorScada.csv')
scada_error = SCADAError(data, 'event_unit','event_start_time','event_end_time','event_type','故障次数')
```

### scada_error.error_analysis()

根据初始化定义的参数，该函数利用 `function` 字段分析 SCADA 故障数据，计算故障次数和停机时间。该功能旨在帮助用户高效管理和评估风机运行状态，确保数据的准确性和可追溯性。

> **参数**

> **使用示例**

```python
scada_error = SCADAError(data, 'event_unit','event_start_time','event_end_time','event_type','故障次数')
scada_error.error_analysis()

T28-04 故障次数6
T29-04 故障次数3
T30-04 故障次数14
```

### scada_error.error_statistical(type,save_flag)

根据初始化时定义的参数，该函数根据 `type` 参数分析 SCADA 系统中的故障或警告数据，并对这些数据进行分类处理。该函数生成多种统计图表，包括各风机的故障类型总统计图、故障类型专门统计图、报警类型统计图以及故障类型分类统计图。根据 `save_flag` 参数的设置，函数可选择性地将这些结果图像保存下来，以供进一步分析和参考。

> 参数：

- **`type`** (str): 故障类型、警告类型
- **`save_flag`** (bool): 分析结果图片保存标志

> **使用示例**

```python
scada_error = SCADAError(data, 'event_unit', 'event_start_time', 'event_end_time', 'event_number', '故障统计')
scada_error.error_statistical('故障',True)

- Start: 2024-04-01 14:12:52, End: 2024-04-01 14:13:00, Fault Code: 351, Duration: 0 days 00:00:08
- Start: 2024-04-02 02:25:41, End: 2024-04-02 02:25:49, Fault Code: 351, Duration: 0 days 00:00:08
- Start: 2024-04-02 03:13:19, End: 2024-04-02 07:23:22, Fault Code: 351, Duration: 0 days 04:10:03
- Start: 2024-04-03 00:31:02, End: 2024-04-03 00:31:10, Fault Code: 351, Duration: 0 days 00:00:08
- Start: 2024-04-03 01:56:54, End: 2024-04-03 07:40:37, Fault Code: 351, Duration: 0 days 05:43:43
- Start: 2024-04-04 01:33:09, End: 2024-04-04 07:32:56, Fault Code: 21, Duration: 0 days 05:59:47
{'变流器故障': [1, 21587.0], '变桨故障': [5, 35650.0], '偏航故障': [0, 0], '主控故障': [0, 0], '发电机故障': [0, 0], '润滑故障': [0, 0], '水冷故障': [0, 0], '其他故障': [0, 0]}
- Start: 2024-04-01 13:27:58, End: 2024-04-06 14:54:27, Fault Code: 310, Duration: 5 days 01:26:29
- Start: 2024-04-06 17:33:22, End: 2024-04-06 17:33:45, Fault Code: 375, Duration: 0 days 00:00:23
{'变流器故障': [0, 0], '变桨故障': [2, 437212.0], '偏航故障': [0, 0], '主控故障': [0, 0], '发电机故障': [0, 0], '润滑故障': [0, 0], '水冷故障': [0, 0], '其他故障': [0, 0]}
- Start: 2024-04-01 10:24:38, End: 2024-04-01 10:25:32, Fault Code: 21, Duration: 0 days 00:00:54
- Start: 2024-04-01 13:13:01, End: 2024-04-01 13:14:31, Fault Code: 21, Duration: 0 days 00:01:30
- Start: 2024-04-01 14:12:51, End: 2024-04-01 15:54:57, Fault Code: 320, Duration: 0 days 01:42:06
- Start: 2024-04-01 19:07:09, End: 2024-04-01 19:07:17, Fault Code: 351, Duration: 0 days 00:00:08
- Start: 2024-04-01 21:35:14, End: 2024-04-01 21:36:40, Fault Code: 21, Duration: 0 days 00:01:26
- Start: 2024-04-01 22:53:32, End: 2024-04-02 07:35:17, Fault Code: 320, Duration: 0 days 08:41:45
- Start: 2024-04-02 12:08:17, End: 2024-04-02 12:09:41, Fault Code: 21, Duration: 0 days 00:01:24
- Start: 2024-04-02 13:58:41, End: 2024-04-02 14:00:10, Fault Code: 21, Duration: 0 days 00:01:29
- Start: 2024-04-02 15:52:25, End: 2024-04-02 15:53:54, Fault Code: 21, Duration: 0 days 00:01:29
- Start: 2024-04-02 17:36:17, End: 2024-04-02 17:37:41, Fault Code: 21, Duration: 0 days 00:01:24
- Start: 2024-04-02 19:00:47, End: 2024-04-02 19:02:10, Fault Code: 21, Duration: 0 days 00:01:23
- Start: 2024-04-02 19:47:23, End: 2024-04-03 07:44:36, Fault Code: 320, Duration: 0 days 11:57:13
- Start: 2024-04-03 13:13:17, End: 2024-04-03 13:14:48, Fault Code: 21, Duration: 0 days 00:01:31
- Start: 2024-04-06 19:56:55, End: 2024-04-06 19:57:01, Fault Code: 223, Duration: 0 days 00:00:06
{'变流器故障': [9, 750.0], '变桨故障': [4, 80472.0], '偏航故障': [1, 6.0], '主控故障': [0, 0], '发电机故障': [0, 0], '润滑故障': [0, 0], '水冷故障': [0, 0], '其他故障': [0, 0]}
```

