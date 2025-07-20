## 0.模板   
- 语言:Python       
```python

# 代码示例
def example_function(param1, param2):

```
----------------------------------------------------------------------------------------------------------------------------------
## 1.将图片倒圆角/美化图标
- 语言:Python   

```python
# python
# 此段代码功能是将图片倒圆角
# time:2025.07.21   rhj
# 关键参数
#         input_path (str): 输入图像的路径，默认为 'resources/imge.png'
#         output_path (str): 输出图像的路径，默认为 'resources/imge_rounded.png'
#         corner_radius (int): 圆角半径，默认为20像素input_path (str): 输入图像的路径，默认为 'resources/imge.png'
#         output_path (str): 输出图像的路径，默认为 'resources/imge_rounded.png'
#         corner_radius (int): 圆角半径，默认为20像素

from PIL import Image, ImageDraw
import os


def round_image_corners(input_path="resources/imge.png", output_path="resources/imge_rounded.png", corner_radius=80):
    """
    将矩形图像的四个角处理为圆角并保存

    参数:
        input_path (str): 输入图像的路径，默认为 'resources/imge.png'
        output_path (str): 输出图像的路径，默认为 'resources/imge_rounded.png'
        corner_radius (int): 圆角半径，默认为20像素

    返回:
        bool: 处理是否成功
    """
    # 检查输入文件是否存在
    if not os.path.exists(input_path):
        print(f"错误: 输入图像不存在: {input_path}")
        return False

    try:
        # 加载图像并转换为RGBA模式以支持透明
        image = Image.open(input_path).convert("RGBA")
        print(f"成功加载图像: {input_path}, 尺寸={image.size}")

        # 创建圆角蒙版
        width, height = image.size
        mask = Image.new("L", (width, height), 0)
        draw = ImageDraw.Draw(mask)
        draw.rounded_rectangle(
            (0, 0, width, height),
            radius=corner_radius,
            fill=255
        )
        print(f"创建圆角蒙版: 尺寸={width}x{height}, 圆角半径={corner_radius}")

        # 应用蒙版到图像
        rounded_image = Image.new("RGBA", image.size)
        rounded_image.paste(image, (0, 0), mask)

        # 确保输出目录存在
        os.makedirs(os.path.dirname(output_path), exist_ok=True)

        # 保存指标保存图像
        rounded_image.save(output_path, "PNG")
        print(f"圆角图像已保存: {output_path}")
        return True
    except Exception as e:
        print(f"处理圆角图像失败: {str(e)}")
        return False


if __name__ == "__main__":
    # 执行圆角处理
    success = round_image_corners()
    if success:
        print("图标已成功处理为圆角版本！")
    else:
        print("图标处理失败，请检查输入文件或路径。")
```
----------------------------------------------------------------------------------------------------------------------------------
