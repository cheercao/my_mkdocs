# YawAnalysis
SCAD系统风机运行数据，偏航分析，包括液压压力分析、风向角度分析、风机当前状态值分析、偏航要求值分析、偏航次数分析、建压速度分析、偏航角度分析

> YawAnalysis(directory_path, trubine_field,hydraulic_pressure = None,angle_of_wind=None,fan_status=None,
>          yaw_require=None,yaw_times=None,build_pressure_speed=None,angle=None)

初始化偏航分析类，通过多线程分析指定目录路径下的文件中的SCADA偏航数据

> 参数：

- **`directory_path`** (str): 

  数据文件的目录路径。

- **`trubine_field`** (str):

   风力发电机的字段名。

- **`hydraulic_pressure`** (str): 

  液压压力的字段名，默认为 `None`。

- **`angle_of_wind`** (str): 

  风向角度的字段名，默认为 `None`。

- **`fan_status`** (str): 

  风机当前状态值的字段名，默认为 `None`。

- **`yaw_require`** (str): 

  偏航要求值的字段名，默认为 `None`。

- **`yaw_times`** (str):

  偏航次数的字段名，默认为 `None`。

- **`build_pressure_speed`** (str):

  建压速度的字段名，默认为 `None`。

- **`angle`** (str): 

  偏航角度的字段名，默认为 `None`。

> **使用示例**

```python
yaw_analysis = YawAnalysis('./SampleData/SecondData',trubine_field = '风机ID',hydraulic_pressure = '液压制动压力',angle_of_wind = '风向绝对值', fan_status = '风机当前状态值',yaw_require = '偏航要求值',yaw_times = '总偏航次数',build_pressure_speed = None, angle = None)
```

> YawAnalysis.analysis()

根据初始化定义的参数，该类分析所有非 `None` 的字段。数据源为SCADA秒级数据，可以处理路径下所有的CSV文件，包括多层级目录中的文件以及压缩在ZIP中的CSV文件。例如如果液压压力字段不为 `None`，则以多线程形式分析风机液压压力。最终结果存储在 `result_dict` 中，通常与 `YawAnalysis.get_result()` 方法配合使用。

> **使用示例**

```python
yaw_analysis.analysis()
result = yaw_analysis.get_result()

{'2 最大液压压力平均值(Pa)': 125.636, '2 最大液压压力(Pa)': 180.3, '2 风向变化总角度(°)': 2557.0, '2 发电状态偏航总次数': 5, '2 发电状态最大偏航时长(秒)': 39, '2 有效数据量': 586, '2 总偏航时间(小时)': 0.04, '2 总偏航次数': 5.0}
```

