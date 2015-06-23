# MinimalSpanningTree.java
import java.lang.Integer;
import java.util.ArrayList;
import java.util.List;
public class MinimalSpanningTree {
	int min = 0;//定义已有节点中，最小的对外路径的权值
	int row = 0;//最小对外路径的，行下标
	int column = 0;//最小对外路径的，列下标
	int x = Integer.MAX_VALUE;//定义一个可看作无穷大的值
	int PathLen = 0;//最短路径变量
	List< Integer > list = new ArrayList<>();//初始化一个容器
	int [][] AdjacencyMatrix = new int[][]{//定义图G的邻接矩阵
			{0,6,1,5,x,x},
			{6,0,5,x,3,x},
			{1,5,0,5,6,4},
			{5,x,5,0,x,2},
			{x,3,6,x,0,6},
			{x,x,4,2,6,0},
	};
	
	/*
	 ********************************************************************************************
	 * 构造最小生成树的方法（步骤如下）：	从第i个节点（第1个节点）出发，找到矩阵里第i行中值最小的元素;
	 * 	                     get   size        list.contains(j)                                                
	 * 1、遍历容器list内所有的元素的值，表示的行的所有元素，找出这些元素极小值（ 除了0 && 列下标 != 遍历过的行的下标 ）                                                                                                       
	 * 2、记录该元素的列下标 ，加入容器List;                                                              
	 * 3、递归：  
	 *        条件：容器内元素个数，小于或者等于图的节点个数时;
	 *        
	 *********************************************************************************************        
	 */
	public void buildTree(){
		//System.out.println("size=" + list.size());//测试容器容量
		min = x;
		for (int i = 0; i < list.size(); i++) {
			//依次扫描容器内各个元素的值list.get(i)，将它们的值作为邻接矩阵点的横坐标，对各行进行遍历
			int min1 = min;//把已经扫描过的行，所得到的最小值，作为本行初始的极小值
			for (int j = 0; j < 6; j++) {
				if (AdjacencyMatrix[list.get(i)][j] <= min1 &&AdjacencyMatrix[list.get(i)][j] != 0 &&  !list.contains(j)) {
					min1 = AdjacencyMatrix[list.get(i)][j];
					row = list.get(i);
					column = j;
				}
				//System.out.println(min1 + "    " +column);//测试代码
			}
			//System.out.println(min1 + "    " +column);//测试代码
			if (min1 < min)  min = min1;
			//System.out.println(min);//测试代码
		}
		this.PathLen += this.min;//遍历完整个容器后，找出当前最短路径，求算当前总路径权值
		System.out.println( " "+(row + 1) + "  ——————" + min + "————> " + (column + 1) );//输出最小生成树的指向关系
		list.add(column);
		if (list.size() < 6)  this.buildTree();//如没遍历完所有节点，即容器容量小于节点数，执行递归
	}
	
	public void displayTree(){
		System.out.println("按时间顺序，加入最小生成树的各个节点依次是： ");
		for (int i = 0; i < list.size(); i++) 
			System.out.print(list.get(i) + 1 + "  ");
			
		
		System.out.println('\n' + "总路径长度为 ： " + this.PathLen);
	}
	

	public static void main(String[] args) {
		MinimalSpanningTree mst = new MinimalSpanningTree();//实例化对象
		mst.list.add(0);//设定初始节点
		//mst.displayTree();
		System.out.println("节点"+"           带权路径       节点");
		mst.buildTree();
		mst.displayTree();
		
	}

}
