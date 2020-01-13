# Some pitfalls when running ROS1 in Windows10
- The usage of "rostopic pub" is not as same as it does under Ubuntu.
    - SOLUTION: replace the single quotes('') with the double quotes("")
- rqt_graph cannot display icons correctly.
    - SOLUTION: Actually, I ignore it.
- rqt_graph cannot draw the arrow which cross other arrows.(I am not sure which situation exactly it failed in.)
    - SOLUTIONS: modify the "edge_item.py" located in "C:\opt\ros\melodic\x64\lib\site-packages\qt_dotgraph\". Find the line contains "while len(coordinates) > 2:", and replace the whole block with:
    ```
    while len(coordinates) > 2:
            # extract triple of points for a cubic spline
            parts = coordinates.pop(0).split(',')
            for i, part in enumerate(parts):
              parts[i] = part.replace('\\\r\n', '')
            point1 = QPointF(float(parts[0]), -float(parts[1]))
            parts = coordinates.pop(0).split(',')
            for i, part in enumerate(parts):
                parts[i] = part.replace('\\\r\n', '')
            point2 = QPointF(float(parts[0]), -float(parts[1]))
            parts = coordinates.pop(0).split(',')
            for i, part in enumerate(parts):
                parts[i] = part.replace('\\\r\n', '')
            point3 = QPointF(float(parts[0]), -float(parts[1]))
            path.cubicTo(point1, point2, point3)
    ```

    