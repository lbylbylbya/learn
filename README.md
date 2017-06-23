# learn
learn
package com.qq.client.view;
import javax.swing.*;

import com.qq.client.model.QqClientConServer;
import com.qq.client.tools.ManageQqChat;

import java.awt.*;
import java.awt.event.*;
import java.net.SocketException;
public class QqFriendList extends JFrame implements ActionListener,MouseListener{
	//把整个JFram做成卡片布局
	CardLayout cl;
	//第一张卡片组件
	JPanel jphy1,jphy2,jphy3;
	JButton jphy_jb1,jphy_jb2,jphy_jb3;
	JScrollPane jsp1;
	String owner;
	//第二张卡片组件
	JPanel jpmsr1,jpmsr2,jpmsr3;
	JButton jpmsr_jb1,jpmsr_jb2,jpmsr_jb3;
	JScrollPane jsp2;
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		//QqFriendList qqFriendList=new QqFriendList();
	}
	public QqFriendList(String owneruId) {
		// TODO Auto-generated constructor stub
		//第一张卡片 
		//三个按钮
		this.owner=owneruId;
		jphy_jb1=new JButton("我的好友");
		jphy_jb2=new JButton("陌生人");
		jphy_jb2.addActionListener(this);
		jphy_jb3=new JButton("黑名单");
		//jphy1显示"好友列表"时，整个界面显示
		jphy1=new JPanel(new BorderLayout());
		//显示50个好友的列表
		jphy2=new JPanel(new GridLayout(50,1,4,4));
		//初始化50个好友
		JLabel []jbls=new JLabel[50];
		for(int i=0;i<jbls.length;i++){
			jbls[i]=new JLabel(i+1+"",new ImageIcon("image\\mm.jpg"),JLabel.LEFT);
			jbls[i].setEnabled(false);
			if(jbls[i].getText().equals(owneruId)){
				jbls[i].setEnabled(true);
			}
			jbls[i].addMouseListener(this);
			jphy2.add(jbls[i]);
		}
		//包围好友列表的
		jsp1=new JScrollPane(jphy2);
		//显示"黑名单"，"陌生人"
		jphy3=new JPanel(new GridLayout(2,1));				
		jphy3.add(jphy_jb2);
		jphy3.add(jphy_jb3);
		//最外围的放入组件
		jphy1.add(jphy_jb1,"North");
		jphy1.add(jsp1,"Center");
		jphy1.add(jphy3,"South");
		//第二张卡片
		//三个按钮
		jpmsr_jb1=new JButton("我的好友");
		jpmsr_jb1.addActionListener(this);
		jpmsr_jb2=new JButton("陌生人");		
		jpmsr_jb3=new JButton("黑名单");
		//jpmsr1"陌生人"时整个界面显示
		jpmsr1=new JPanel(new BorderLayout());
		//显示20个陌生人的列表
		jpmsr2=new JPanel(new GridLayout(20,1,4,4));
		//初始化20个陌生人
		JLabel []jbls2=new JLabel[20];
		for(int i=0;i<jbls2.length;i++){
			jbls2[i]=new JLabel(i+1+"",new ImageIcon("image\\mm.jpg"),JLabel.LEFT);
			jbls2[i].addMouseListener(this);
			jpmsr2.add(jbls2[i]);
		}
		//包围陌生人列表的
		jsp2=new JScrollPane(jpmsr2);
		//显示"我的好友"，"陌生人"
		jpmsr3=new JPanel(new GridLayout(2,1));				
		jpmsr3.add(jpmsr_jb1);
		jpmsr3.add(jpmsr_jb2);
		//最外围的放入组件
		jpmsr1.add(jpmsr3,"North");
		jpmsr1.add(jsp2,"Center");
		jpmsr1.add(jpmsr_jb3,"South");
		//对整个JFrame设置成卡片布局
		cl=new CardLayout();
		this.setLayout(cl);
		//放入卡片
		this.add(jphy1,"1");
		this.add(jpmsr1,"2");	
		this.setSize(200,400);
		this.setTitle(owneruId);
		this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		this.setVisible(true);
	}
	@Override
	public void actionPerformed(ActionEvent e) {
		// TODO Auto-generated method stub
		if(e.getSource()==jphy_jb2){
			cl.show(this.getContentPane(), "2");
			//不能直接this，会报错，因为不能对最外层show
		}else if(e.getSource()==jpmsr_jb1){
			cl.show(this.getContentPane(), "1");
		}
	}
	@Override
	public void mouseClicked(MouseEvent e) {
		// TODO Auto-generated method stub
		//响应用户双击的事件，并得到好友的编号
		if(e.getClickCount()==2){
			String friendNo=((JLabel)e.getSource()).getText();
			QqChat qqChat=new QqChat(owner,friendNo);
			//把聊天界面加入到管理类中
			ManageQqChat.addQqChat(this.owner+""+friendNo, qqChat);
		}
	}
	@Override
	public void mouseEntered(MouseEvent e) {
		// TODO Auto-generated method stub
		JLabel jl=(JLabel)e.getSource();
		jl.setForeground(Color.red);
	}
	@Override
	public void mouseExited(MouseEvent e) {
		// TODO Auto-generated method stub
		JLabel jl=(JLabel)e.getSource();
		jl.setForeground(Color.black);
	}
	@Override
	public void mousePressed(MouseEvent e) {
		// TODO Auto-generated method stub
		
	}
	@Override
	public void mouseReleased(MouseEvent e) {
		// TODO Auto-generated method stub
		
	}
}
