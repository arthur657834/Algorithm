openlist:
可以到达的格子

closelist:
已经到达的格子

F=G+H
G: 从起点到当前格的步数
H: 当前格到目标格的步数(不考虑障碍)

```java
public Node aStarSearch(Node start, Node end) {
    // 把起点加入 open list  
    openList.add(start);
    //主循环，每一轮检查一个当前方格节点
    while (openList.size() > 0) {
        // 在OpenList中查找 F值最小的节点作为当前方格节点
        Node current = findMinNode();
        // 当前方格节点从open list中移除
        openList.remove(current);
        // 当前方格节点进入 close list
        closeList.add(current);
        // 找到所有邻近节点
        List<Node> neighbors = findNeighbors(current);
        for (Node node : neighbors) {
            if (!openList.contains(node)) {
                //邻近节点不在OpenList中，标记父亲、G、H、F，并放入OpenList
                markAndInvolve(current, end, node);
            }
        }
        //如果终点在OpenList中，直接返回终点格子
        if (find(openList, end) != null) {
            return find(openList, end);
        }
    }
    //OpenList用尽，仍然找不到终点，说明终点不可到达，返回空
    return null;
}
```
