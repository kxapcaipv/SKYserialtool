### 产品介绍

**SKYserialtool**是一个功能强大的实时波形绘制和数据监测应用程序，专为需要高效实时数据处理和图形展示的用户设计。它结合了Qt框架和QCustomPlot库，提供了一个用户友好的界面，可以在串口数据流中实时绘制和分析数据。

### 主要功能
1. **多通道数据可视化**：
    - 支持最多15个通道的串口数据可视化显示。
    - 支持多达六个通道的数据可视化，每个通道都可以在独立的图表中显示数据。
    - 用户可以为每个通道设置不同的图表名称、数据前缀和后缀，使得数据处理更加灵活和直观。
2. **混合绘制和独立绘制模式切换**：
    - **多通道混合绘制模式**：适用于比较多通道数据差异的场景，可以在一个图表上连续显示来自多个通道的多个数据点。
    - **多通道独立模式**：适用于同时处理来自多个通道的数据。数据会被自动分配到相应的通道图表中。
3. **数据采样与绘制**：
    - 当数据量超过设定的缓冲区大小时，系统会自动进行数据采样，以提高绘图性能并保持界面的流畅。
    - 支持动态绘制和自动调整X轴和Y轴的范围，以适应数据变化。
4. **图表操作**：
    - 提供缩放和拖动功能，用户可以通过交互操作轻松浏览数据。
    - 支持自动和手动模式，用户可以选择是否让图表自动调整轴范围。
5. **实时数据接收与处理**：
    - 可以通过串口实时接收数据，并在图表中即时显示。
    - 支持数据的动态更新和图表的实时重绘，确保用户能够获取到最新的数据信息。
6. **数据保存和清除**：
    - 支持将数据保存为CSV格式文件，方便后续的数据分析和记录。
    - 提供清除按钮，用户可以快速清除当前显示的图表数据。
7. **串口配置**
    - 支持多种串口配置选项，包括波特率、数据位、停止位、奇偶校验和流控制。用户可以根据实际需要选择合适的配置。
8. **串口数据监控**：
    - 提供串口数据监控窗口，用户可以查看串口接收到的原始数据和解析后的数据。
    - 支持清除监控窗口中的数据，保持界面的整洁。
### 技术实现
- **用户界面**：使用Qt框架创建图形用户界面，结合QCustomPlot库进行数据绘图和图表交互。
- **多线程处理**：数据处理和绘图在独立的线程中进行，确保界面响应迅速且不被阻塞。
- **数据解析**：支持从串口接收的数据进行解析，并将数据映射到不同的图表中进行展示。
- **配置管理**：提供灵活的配置选项，允许用户自定义图表的显示方式和数据处理方式。

### 串口协议
#### 1. 多通道混合绘制模式 
**数据格式**： 在多通道模式下，每行数据表示多个通道的单一数据点。数据格式如下：

```
test data:value1,value2,...,valueN\n
```
- `test data`：数据标识，可以换成时间戳方便查看。 
- `value1`, `value2`, ..., `valueN`：数据点的值，按照实际数据顺序排列。 
- `\n`：换行符，数据按行识别
- 例**：
```
test data:1.23,2.34,3.45 1,4.56,5.67,6.78 2,7.89,8.90,9.01\n
```
**说明**：

- `value1`数据属于通道0，包含1个数据点（1.23）。
- `value2`数据属于通道1，包含1个数据点（2.34）。
- `value3`数据属于通道2，包含1个数据点（ 3.45）。

#### 2. 多通道独立绘制模式

**数据格式**：

在多通道独立绘制模式下，每行数据表示单个通道的多个数据点。数据格式如下：
```
channel_prefix,value1,value2,...,valueN,channel_suffix
```
- `channel_prefix`：数据的前缀，用于标识数据类型或来源，通常是固定的字符串。
- `value1`, `value2`, ..., `valueN`：数据点的值，按照实际数据顺序排列。
- `channel_suffix`：数据的后缀，通常是固定的字符串，用于标识数据的结束或其他信息。

**示例**：
```
prefix,1.23,2.34,3.45,suffix
prefix,4.56,5.67,6.78,suffix
prefix,7.89,8.90,9.01,suffix
```
**说明**：

- 每行数据表示一个数据包，其中包括一个固定的前缀和后缀。
- 数据点（1.23, 2.34, 3.45）被依次传输到图表上。
- 前缀和后缀可以根据需要进行自定义。

---

## 数据发送指南

1. **确定模式**：根据实际需求选择通道模式。

2. **格式化数据**：按照所选模式的数据格式准备数据。

3. **发送数据**：
   - 使用串口通信工具或编程接口将格式化的数据通过串口发送至主机。
   - 确保数据的分隔符和格式正确，以便主机能够正确解析数据。

4. **检查通信设置**：确保下位机的串口配置（如波特率、数据位、停止位、奇偶校验）与主机设置一致。

5. **数据验证**：发送数据后，检查主机是否能正确接收和显示数据。如发现问题，检查数据格式和串口配置是否正确。

---

这种协议说明可以帮助下位机正确地发送数据，并确保主机能够正确接收和解析数据。如果有进一步的需求或需要对协议进行调整，请随时告知！
