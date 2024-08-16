# GeneratorPerformances

`GeneratorPerformance` 类用于初始化发电性能分析绘图。通过指定绘图数据、X轴字段、Y轴字段、X轴和Y轴标签，以及绘制的具体曲线类型，该类可以生成多种性能分析曲线。这些曲线包括转矩-转速曲线、转速-桨距角曲线、风速-桨距角曲线、风速-转速曲线以及风速-功率曲线。这些图表为评估和优化发电机性能提供了直观的数据可视化工具。

### GeneratorPerformance(data, filed1,filed2,xlabel,ylabel,function)

初始化 SCADA 数据发电性能分析类后，可以通过指定所需绘制的曲线类型，以及对应的 X 轴数据、Y 轴数据、X 轴标签和 Y 轴标签，生成相应的性能分析图表。该类不仅支持灵活定义不同类型的曲线，还可以将生成的图表保存下来，以便后续分析和参考。

> 参数：

- **`data`** (DataFrame): 用于绘图的数据。
- **`filed1`** (str): X轴字段。
- **`filed2`** (str): Y轴字段。
- **`xlabel`** (str): X轴标签。
- **`ylabel`** (str): Y轴标签。
- **`function`** (str): 用于绘制具体曲线的函数，支持的曲线包括转矩-转速曲线、转速-桨距角曲线、风速-桨距角曲线、风速-转速曲线、风速-功率曲线等。

> **使用示例**

```python
data = pd.read_csv('wtai_dt/SampleData/SCADA_ten_min/SampleScada.csv')
power = PowerGenerationStatistics(data, 'wt_id','tal_ac_pw_gen', 'time', 'daily')
```

### generator_performance.Plot(image_name)

根据初始化定义的参数，该函数利用 `function` 字段分析 SCADA 故障数据，绘制发电性能曲线，根据image_name参数，将绘图保存。

> **参数**

- **`image_name`** (str): 绘图保存文件名。

> **使用示例**

```python
generator_performance = GeneratorPerformance(data, 'wind_speed','active_power','风速','功率','风速-功率曲线')
generator_performance.Plot('风机 1 风速-功率曲线')
generator_performance = GeneratorPerformance(data, 'generator_torque', 'wheel_rpm', '转矩', '转速', '转矩-转速曲线')
generator_performance.Plot('风机 1 转矩-转速曲线')
generator_performance = GeneratorPerformance(data, 'wheel_rpm', 'blade1_angle', '转速', '桨距角', '转速-桨距角曲线')
generator_performance.Plot('风机 1 转速-桨距角曲线')
generator_performance = GeneratorPerformance(data, 'wind_speed', 'blade1_angle', '风速', '桨距角', '风速-桨距角曲线')
generator_performance.Plot('风机 1 风速-桨距角曲线')
generator_performance = GeneratorPerformance(data, 'wind_speed', 'wheel_rpm', '风速', '转速', '风速-转速曲线')
generator_performance.Plot('风机 1 风速-转速曲线')
generator_performance = GeneratorPerformance(data, 'wind_speed', 'wind_speed', '风速', '风速', '风速曲线')
generator_performance.Plot()
```