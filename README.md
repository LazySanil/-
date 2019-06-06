package deskball;

import java.awt.*;
import javax.swing.*;

public class DeskBall extends JFrame {
	
	Image ball = Toolkit.getDefaultToolkit().getImage("images/ball.png");
	Image desk = Toolkit.getDefaultToolkit().getImage("images/desk.jpg");
	
	double x = 100;	//小球的横坐标
	double y = 100;	//小球的纵坐标
//	boolean right = true;	//表示方向向右
	double degree = 3.14/3;	//表示弧度60度
	
	//画窗口的方法
	public void paint(Graphics g) {
		g.drawImage(desk, 0, 0, null);
		g.drawImage(ball, (int)x, (int)y, null);
		
		//这里是三角函数的知识，忘记了可以自己翻翻书或者百度一下
		x = x + 10 * Math.cos(degree);
		y = y + 10 * Math.sin(degree);
		
		//碰到上下边界时反弹
		if(y>500-40-30 || y<40+40) {//其中500是窗口高度，40是球桌边框的宽度，30是球的直径，最后一个40是标题栏的宽度
			degree = -degree;
		}
		
		//碰到左右边界时反弹
		if(x>856-40-30 || x<40) {
			degree = 3.14 - degree;
		}
		
//		if(right) {
//			x = x + 10;
//		}else {
//			x = x - 10;
//		}
//		
//		if(x>856-40-30) {	//856是窗口的宽度，40是球桌边框的宽度，30是小球的直径
//			right = false;
//		}
//		
//		if(x<40) {	//40是球桌边框的宽度
//			right = true;
//		}
	}
	
	
	//窗口加载
	void launchFrame() {
		//指的是宽和高各为300px
		setSize(856,500);
		//指的是坐标的位置 这里的坐标是从窗口距离屏幕左上角开始算起的
		setLocation(50,50);
		setVisible(true);
		

		//反复重画窗口
		while(true) {
			//重画方法
			repaint();

			try {
				//每次画完暂停40ms
				Thread.sleep(40);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
		
		
	}
	
	//main方法是程序执行的入口
	public static void main(String[] args) {
		DeskBall game = new DeskBall();
		game.launchFrame();
		
		System.out.println();
	}
	
}

