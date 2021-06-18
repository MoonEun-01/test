package Tetris;
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class TetrisEx extends JFrame 
{
   Container c = getContentPane();	//컨테이너 생성
   TetrisPanel TP = new TetrisPanel();	//게임을 진행할 패널
   JDialog JD = new JDialog();	//최종점수를 띄울 JDialog
   TetrisThread th;	//테트리스 스레드, 블록이 떨어지는 속도
   
   static int blocksize = 20;	//블록사이즈
   
   int End = 0;
   int random = 0;	//  랜던값 저장하여 사용할 변수
   int random2 = (int)(Math.random()*7);	//7가지모양의 블럭중 랜덤으로 생성
   //int randomColor = 0, randomColor2 = 0; //블록 색상을 통일하기 위해 추가
   int score = 0; //점수 초기화
   
   int Stop_Count = 0;	//버튼글자 위해서
   
   int wid=100;	//블록을 움직일 가로값
   int hgt= 0;	//블록을 움직일 세로값
   int rotation = 0;	// 블럭 방향값
   
   boolean limit = false;	//벽에 충돌하는지 검사하기 위해 
   
   int curX[]= new int[4], curY[] = new int [4]; // 블록들의 좌표 저장
   
   int blocks[][][][]  = //int blocks[블록모양7][방향4][y][x]
	      {
	         {
	            //■
	            //■■■
	            {
	               {0,0,0,0},
	               {1,0,0,0},
	               {1,1,1,0},
	               {0,0,0,0}
	            },
	            {
	               {0,1,1,0},
	               {0,1,0,0},
	               {0,1,0,0},
	               {0,0,0,0}
	            },
	            {
	               {1,1,1,0},
	               {0,0,1,0},
	               {0,0,0,0},
	               {0,0,0,0}
	            },
	            {
	               {0,0,1,0},
	               {0,0,1,0},
	               {0,1,1,0},
	               {0,0,0,0}
	            }
	         },
	         {
	               //  ■
	               //■■■
	            {
	               {0,0,0,0},
	               {0,0,1,0},
	               {1,1,1,0},
	               {0,0,0,0}
	            },
	            {
	               {0,1,0,0},
	               {0,1,0,0},
	               {0,1,1,0},
	               {0,0,0,0}
	            },
	            {
	               {0,0,0,0},
	               {1,1,1,0},
	               {1,0,0,0},
	               {0,0,0,0}
	            },
	            {
	               {0,1,1,0},
	               {0,0,1,0},
	               {0,0,1,0},
	               {0,0,0,0}
	            }
	         },
	         {
	               //  ■■
	               //  ■■
	            {
	               {0,0,0,0},
	               {1,1,0,0},
	               {1,1,0,0},
	               {0,0,0,0}
	            },
	            {
	               {0,0,0,0},
	               {1,1,0,0},
	               {1,1,0,0},
	               {0,0,0,0}
	            },
	            {
	               {0,0,0,0},
	               {1,1,0,0},
	               {1,1,0,0},
	               {0,0,0,0}
	            },
	            {
	               {0,0,0,0},
	               {1,1,0,0},
	               {1,1,0,0},
	               {0,0,0,0}
	            }
	         },
	         {
	               // ■■■■
	            {
	               {0,0,0,0},
	               {0,0,0,0},
	               {1,1,1,1},
	               {0,0,0,0}
	            },
	            {
	               {0,1,0,0},
	               {0,1,0,0},
	               {0,1,0,0},
	               {0,1,0,0}
	            },
	            {
	               {0,0,0,0},
	               {0,0,0,0},
	               {1,1,1,1},
	               {0,0,0,0}
	            },
	            {
	               {0,1,0,0},
	               {0,1,0,0},
	               {0,1,0,0},
	               {0,1,0,0}
	            }
	         },
	         {
	                //■
	               //■■■
	            {
	               {0,0,0,0},
	               {0,1,0,0},
	               {1,1,1,0},
	               {0,0,0,0}
	            },
	            {
	               {0,1,0,0},
	               {0,1,1,0},
	               {0,1,0,0},
	               {0,0,0,0}
	            },
	            {
	               {0,0,0,0},
	               {1,1,1,0},
	               {0,1,0,0},
	               {0,0,0,0}
	            },
	            {
	               {0,1,0,0},
	               {1,1,0,0},
	               {0,1,0,0},
	               {0,0,0,0}
	            }   
	         },
	         {
	                //  ■■
	                //   ■■
	            {
	               {0,0,0,0},
	               {1,1,0,0},
	               {0,1,1,0},
	               {0,0,0,0}
	            },
	            {
	               {0,0,1,0},
	               {0,1,1,0},
	               {0,1,0,0},
	               {0,0,0,0}
	            },
	            {
	               {0,0,0,0},
	               {1,1,0,0},
	               {0,1,1,0},
	               {0,0,0,0}
	            },
	            {
	               {0,0,1,0},
	               {0,1,1,0},
	               {0,1,0,0},
	               {0,0,0,0}
	            }
	         },
	         {
	                //  ■■
	               //  ■■
	            {
	               {0,0,0,0},
	               {0,1,1,0},
	               {1,1,0,0},
	               {0,0,0,0}
	            },
	            {
	               {0,1,0,0},
	               {0,1,1,0},
	               {0,0,1,0},
	               {0,0,0,0}
	            },
	            {
	               {0,0,0,0},
	               {0,1,1,0},
	               {1,1,0,0},
	               {0,0,0,0}
	            },
	            {
	               {0,1,0,0},
	               {0,1,1,0},
	               {0,0,1,0},
	               {0,0,0,0}
	            }   
	         }
	   };
   
   
   /*
    * 전체는 세로 21 가로 12지만 블록이 움직이는 공간은 세로 19 가로 11
    * 
    * 수정한 부분
    * 맵 크기 수정 21*12에서 23*13로
    * 맵이 너무 작아서 어렵고 단순하고 재미없다
    * 좀 더 크게 구현
    */
   int[][] gameboard = {	//게임맵 
		   			 {1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1},
		     		 {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
		     		 {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
		     		 {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1},
                     {1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1}};

   JButton btn = new JButton("Replay?");	//JDialog로 뛰울 창에 넣을 재시작버튼
   
   /*
    * 추가한 부분
    * 
    * 멈춤 버튼(클릭하면 START로 바뀜)
    */
   JButton btn_Stop = new JButton("STOP"); // stop버튼, 게임멈춤
   
   
   JLabel lbl = new JLabel();	//점수 레이블
   JLabel lbl2 = new JLabel();	//게임 진행중 현재 점수 출력할 레이블
   JLabel JumSooText = new JLabel(); //점수 뒤에 ~점이라고 적을 레이블 (추가)
   
   TetrisEx()
   {
      setTitle("테트리스");
      setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);	//프로세스종료
      setLayout(null);	//레이아웃 관리자를 사용하지 않음
      
      TP.setSize(700, 700);	//패널 사이즈 700*700
      add(TP);	//패널추가
      
      th = new TetrisThread();	//테트리스 스레드 생성
      
      // JDialog 
      JD.setTitle("GameOver");	// 글자 변경 : 점수 -> 최종점수 -> GameOver
      JD.setSize(240,190);	//dialog창 크기 240*190
      JD.setLayout(new FlowLayout(FlowLayout.CENTER, 150, 30));//중앙정렬, 픽셀단위 좌우:150, 상하:30 띄움
      
      
      lbl.setFont(new Font("나눔고딕",Font.PLAIN,15));
      lbl2.setText("★ 현 재  점 수 ★");	//게임진행될 때 오른쪽에다가 뛰울 점수 레이블
      lbl2.setFont(new Font("나눔고딕",Font.PLAIN,15));	//폰트는 나눔고딕, 크기 15
      
      /* 
       * 추가한 부분
       * 글자 색상 변경 (검은배경에는 흰글씨로)
       */ 
      lbl2.setForeground(Color.WHITE);
      
      
      TP.addKeyListener(new KeyAdapter()	//이동키 입력 이벤트리스너
      {
            public void keyPressed(KeyEvent e){	
               int keyCode = e.getKeyCode();	//조작키 입력받음
                      
               /*
                * 수정한 부분
                * 기존 : 화살표 방향키만 입력
                * 수정 : 화살표 방향키 + WASD 추가
                */
               if(keyCode == KeyEvent.VK_UP || keyCode == KeyEvent.VK_W)	//윗 방향키 눌렀을 때
                  TP.moveUp();
               if(keyCode == KeyEvent.VK_DOWN || keyCode == KeyEvent.VK_S)	//아래 방향키 눌렀을 때
                  TP.moveDown();
               if(keyCode == KeyEvent.VK_LEFT || keyCode == KeyEvent.VK_A)	//왼쪽 방향키 눌렀을 때
                  TP.moveLeft();
               if(keyCode == KeyEvent.VK_RIGHT || keyCode == KeyEvent.VK_D)	//오른쪽 방향키 눌렀을 때
                  TP.moveRight();
               
               /*
                * 추가한 부분
                * 스페이스바를 눌렀을 경우
                * 아래로 바로 내려가서 붙이도록 함
                */
               if(keyCode == KeyEvent.VK_SPACE)
               {
            	   TP.moveHardDrop();
               }
               
            }
         });
      
      btn.addActionListener(new ActionListener()	//replay버튼 액션리스너
      {
         public void actionPerformed(ActionEvent e)
         {
            limit = false;
            for(int y=1; y<22;y++)	//여기 원래 y=0이었음
               for(int x=1; x<12; x++)
                  gameboard[y][x] =0 ;
            score =0;
            wid =100; hgt = 0;
            
            JD.dispose();//replay버튼 누르면 최종점수창 다이얼로그 메모리 제거
         }
      });
      
      
      
      /*
       * 추가한 부분
       * 정지버튼을 누르면 정지가 되면서 버튼의 텍스트가 START로 변경
       * 이후 START버튼을 누르면 다시 실행하면서 STOP으로 버튼의 텍스트를 변경
       */
      btn_Stop.addActionListener(new ActionListener() //STOP-START버튼 액션리스너
      {
          public void actionPerformed(ActionEvent e) 
          {
              btn_Stop.setVisible(true);
              btn_Stop.setLocation(200,300);
              TP.add(btn_Stop);
              if(btn_Stop.getText().equals("STOP")) 
              {
                  th.suspend();	//쓰레드 일시정지
                  btn_Stop.setText("START");
              }
              else 
              {
            	  btn_Stop.setText("STOP");
                  th.resume();	//일시정지된 쓰레드를 실행대기상태로 만든다(재시작)
              }
          }
      });
      
      /*
       * 수정한 부분
       * 백그라운드 색상 흰색에서 검정으로 수정
       * TP.setBackground(Color.WHITE); -> TP.setBackground(Color.BLACK);
       * 흰 배경은 너무 밝아서 눈 아픔
       */
      TP.setBackground(Color.BLACK);
      setSize(530, 580);	//TP 530*580
      setVisible(true);
      

      // 화면 중앙 정렬
      Dimension frameSize = this.getSize();	//디맨션객체에 윈도우창의 사이즈를 받아온다
      Dimension screenSize = Toolkit.getDefaultToolkit().getScreenSize();	//디멘션객체에 모니터 해상도를 받아온다
      setLocation((screenSize.width - frameSize.width)/2, (screenSize.height - frameSize.height)/2);	//프로그램이 시작되면 화면 정가운데(/2)에 표시한다
      JD.setLocation((screenSize.width - frameSize.width)/2 + 220, (screenSize.height - frameSize.height)/2 +220); //다이아로그도 정가운데에서 +220에 위치하도록한다
      
      TP.requestFocus(true);
      th.start();
   }
   
   
   class TetrisPanel extends JPanel
   {
      public void paintComponent(Graphics g)
      {
         
         int cnt = 0 , cnt2 = 0;	//바닥에 닿았는지 카운트 하기 위한 변수
        
         TP.requestFocus(true);		//setFocusavle이 true로 설정된 컴포넌트가 포커스를 달라고 요청.
         
         super.paintComponent(g);	//패널의 배경색을 지정할 수 있는 메소드
         							//drawRext(x,y,w,h), drawOval(x,y,w,h), fillRect, fillOval 등이 있음
         							//해당 소스코드에서는 3차원 사각형씀(벽면디자인(draw), 블록(fill))
         
         lbl2.setLocation(340,120);	//"점수"글자 레이블 위치
         							//(353,120)에서 (340, 120)으로 수정
         TP.add(lbl2);	//"점수" 글자 레이블을 패널에 붙임
         
         lbl.setLocation(370,150);	// score*100 글자 레이블 위치
         							//(365, 150)에서 (370,150)으로 수정
         lbl.setForeground(Color.WHITE);	//글자색 검정으로(추가)
         TP.add(lbl);	//score레이블 패널에 붙임
         lbl.setText(Integer.toString(score*100));	//점수에 100곱해서 100단위로 점수 계산하게 함
         
         
         /*
          * 추가한 부분
          * 정지 및 재시작 버튼
          */
         btn_Stop.setLocation(340, 250);
         TP.add(btn_Stop);
         btn_Stop.setFont(new Font("나눔고딕", Font.BOLD, 15));
         btn_Stop.setSize(100, 40);

         
         /*
          * 점 글자 레이블 추가
          * 
          * 21.06.13 오류 발생
          * TP에 레이블 추가하는건데
          * 게임 종료 후 JD가 깜빡깜빡거리는 에러가 발생
          * 아래 소스코드를 넣으니 깜빡깜빡거리고 안 넣으면 문제가 발생하지 않음
          * 
          * 21.06.18
          * 오늘 시작 버튼 다이얼로그 하나 더 추가했는데 이제는 그냥 깜빡깜빡거리는 에러가 생겼다..
          * 어딜 수정해야 할지 모르겠다
          */
         
         JumSooText.setText("     점");	//score뒤에 '점' 붙임
         JumSooText.setLocation(400, 150);	// 나중에 Dimension이용해서 lbl(score)레이블이 늘어나면
         									// JumSoo레이블도 오른쪽으로 이동하여 몇만점이 나와도 '점'글자와 점수레이블이 겹치지 않게 구현할 것
         JumSooText.setForeground(Color.WHITE);
         JumSooText.setFont(new Font("나눔고딕",Font.PLAIN,14));
         TP.add(JumSooText);	//'점'글자 레이블 패널에 붙임
         
         /*
          * 추가한부분
          * 블록들의 색상 랜덤으로 결정하여 출력
          * 
          * 원래 목적은 블록모양이 random2에 저장되었으니까 random2숫자에 맞춰서 색을 출력하면 될 것이라고 생각해서
          * 그냥 이렇게 적었더니 NEXT블럭도 같은 색상으로 출력이 된다.
          * 이후 run block(현재 움직이는 블럭)은 next블럭의 색상을 따라간다.
          * 
          */
         switch(random2)	//블록의 색상
         {
         case 0:
        	 	g.setColor(Color.RED);
        	 	break;
         case 1:
         	g.setColor(Color.ORANGE);
         	break;
         case 2:
         	g.setColor(Color.YELLOW);
         	break;
         case 3:
         	g.setColor(Color.GREEN);
         	break;
         case 4:
           	g.setColor(Color.BLUE);
           	break;
         case 5:
           	g.setColor(Color.PINK);
           	break;
         case 6:
           	g.setColor(Color.WHITE);
           	break;
         }
         
         blockLookAhead(g);	// NextBlock 출력    
          
         gameOverCheck();// 벽이 천장에 닿으면 게임 오버
                
         removeBlock(cnt, cnt2, g);// 한 행이 모두 블록으로 채워진 경우 블록들 제거(채워지지않은 경우 블록 떨어지도록)
         
         blockToWall();// 블록이 벽에 착지하면 블록->벽으로 변환(떨어지는 블록 초기화)
         
         makeBlock(g);// 고정 벽(바닥에 닿은 벽)을 생성
         
         makeBorder(g);// 테두리 생성
       
         if(End == 1)
         {
            random2 = (int)(Math.random()*7);
            End = 0;
         }
      }
      
      public void blockLookAhead(Graphics g)	// Next Block 미리 보여줌
      {	
         for(int a = 0; a<4 ;a++)	//y값
         {
              for(int b = 0; b<4;b++)//x값
              {
                 if(blocks[random2][0][a][b] == 1)
                 {                	 
                	 //블록 디자인은 3D형식을 사용
                	 // C언어에서는 ■를 사용하여 블록을 표시했는데
                	 // 자바에서는 GUI - fill3DRect를 이용하여 블록을 표현함
                	 //x,y,w,h,볼록(t)/오목(f)
                    g.fill3DRect(b*blocksize+120, a*blocksize, blocksize, blocksize, true);                    
                 }
              }
          }
      }
      
      public void gameOverCheck()	//블록이 천장에 닿았는가
      {
         for(int x=1; x<12; x++)
         {
             if(gameboard[1][x]==1)	//블록이 천장에 닿았을 경우
             {
                limit = true;	//벽 충돌 -> true
                
                //lbl.setLocation(50,50);
                
                lbl.setForeground(Color.BLACK);	//글자색 검정으로(추가)
                								//패널에서 쓰던 점수레이블을 다이어로그에 붙임
                JD.add(lbl);	//JDialog에 최종 점수 글자 레이블 붙임
                JD.add(btn);	//JDialog에 replay?버튼 붙임
               
                //btn.setLocation(50,30);
                
                JD.setVisible(true);	// 최종 점수창 보이도록 설정
             }
         }
      }
      
      public void removeBlock(int cnt, int cnt2, Graphics g)	//블록이 한 줄 채운 경우 지우는 메소두
      {	
         for(int y = 1;y<22;y++)
         {
             for(int x =1; x<12 ; x++)
             {
                if(gameboard[y][x] == 1)
                {
                   cnt2++;	//블록이 바닥에 닿았을 경우 +1을 함
                }
             }
             if(cnt2 == 11)//맵에서 블록이 움직일 수 있는 공간은 가로 11이므로 cnt가 11이 되면 한줄 채운것임
             {	
                for(int i=y;i>1;i--)
                   for(int j=1;j<13;j++)
                   {
                      gameboard[i][j] = 0;	//채운 줄은 0으로 초기화 하고
                      gameboard[i][j] = gameboard[i-1][j];	//그 윗줄[i-1]은 아래로 한칸씩 내림
                   }
               score++;	//한줄 채웠으니까 100점 획득(출력할때 *100 함)
             }else{
                blockDown(cnt,g); // 한 행이 모두 블록으로 채워지지 않을 때만 블록이 내려가도록 함
             }
             cnt2 = 0 ;//11카운트 한 것 0으로 초기화
          }
      }
      
      public void makeBlock(Graphics g) //떨어진 블록 벽으로 고정
      {
         g.setColor(Color.GRAY);	//색상은 회색으로 해서 돌 느낌이 나도록 함
         
          for(int y=1; y<22;y++)
          {
             for(int x=1; x<12; x++)
             {
                if(gameboard[y][x]== 1)	//게임보드가 1인경우(블록으로 채워진 경우)
                {
                   g.fill3DRect( x*blocksize+20, y*blocksize+60, blocksize, blocksize, true);
                }
             }
          }
      }
      
      public void blockDown(int cnt, Graphics g) //자동으로 블록이 아래로 떨어짐
      {	
         for(int j = 0; j<4 ;j++)
         {
              for(int k = 0; k<4;k++)
              {
                 if(blocks[random][rotation][j][k] == 1)
                 {
                    curX[cnt] = ((k*blocksize)+wid)/blocksize;
                    curY[cnt] = ((j*blocksize)+hgt)/blocksize;//curX,Y[0][1][2][3]에 좌표 4개 저장
                    
                    g.fill3DRect(curX[cnt]*blocksize+20, curY[cnt]*blocksize+60, blocksize, blocksize, true);
                    
                    cnt ++;
                 }
              }
           }
      }
      
      
      // 떨어진 블록(회색)이 벽이 되었는지(0이 1이 되었는지) 검사
      // 벽이 되면 wid=120, hgt=0 으로 블록 초기화, rotation도 초기화 
      public void blockToWall()
      {
         try{
         for(int z = 0; z<4 ; z++)
              if(gameboard[curY[z]+1][curX[z]] == 1)
                    for (int j= 0; j<4;j++)
                    {
                          gameboard[curY[j]][curX[j]] = 1;
                          wid =100; 
                          hgt =0;
                          End = 1;
                          rotation = 0;
                          random = random2;
                    }
         }catch(ArrayIndexOutOfBoundsException e){ System.out.println("Error");	//ArrayIndexOutOfBoundsException : 배열의크기보다 큰 인덱스를 사용하면 발생
         for(int i=0; i<4 ; i++)
               System.out.print("("+curY[i]+","+curX[i]+")");
            System.out.println();}
        
         
      }
      
      // 왼쪽 벽에 충돌하면 못 움직이도록(뚫고나가지 않도록)
      public int collision_LEFT(){
         for(int i=0; i<4; i++){
            if(gameboard[curY[i]][curX[i]-1] == 1)  // 충돌 시 1 반환
               return 1;
         }
         return 0; // 충돌하지 않으면 0 반환
      }
      
      // 오른쪽 벽에 충돌하면 못 움직이도록(뚫고나가지 않도록)
      public int collision_RIGHT(){

         for(int i=0; i<4; i++){
            if(gameboard[curY[i]][curX[i]+1] == 1)   // 충돌 시 1반환
               return 1;
         }
         return 0; // 충돌하지 않으면 0반환
      }
      
      /*
       * 추가한 부분
       * 위쪽 벽에 충돌하면 못 움직이도록 함
       */
      public int collision_UP()
      {
    	  for(int i=0; i<4; i++)
    	  {
    		  /*
    		   * 21.06.18
    		   * if(gameboard[curY[i]-1][curX[i]] == 1)을 하면 벽을 뚫고 회전이 한번만 되다가
    		   * 한칸 아래로 내려가면 회전이 가능하고
    		   * 
    		   * if(gameboard[curY[i]-2][curX[i]] == 1)를 하면 벽을 뚫지는 않는데
    		   * 한칸 아래로 내려가면 회전이 한번만 가능하고
    		   * 한칸 더 아래로 내려가면 회전이 계속 가능함
    		   * 
    		   * 21.06.18
    		   * gameboard의 천장부분을 1000...0001에서 1111...1111로 교체
    		   * 이제 오류 없이 작동함
    		   */
    		  if(gameboard[curY[i]][curX[i]]==1)	//블록이 천장에 닿았을 경우
                  return 1; // 충돌시 1반환
            }
            return 0; // 충돌하지 않으면 0반환
      }
      
      // curX,Y에 다음 회전 도형의 절대좌표를 모두 기록해두고, 만약 오른쪽이나 왼쪽 X좌표1,2칸 안에 벽이 있으면 그만큼 오른쪽 혹은 왼쪽으로 밀어서 배치
      public void rotationCheck()
      {
       // curX,Y에 다음 회전 도형의 절대좌표를 모두 기록해두고, 밑에 구문에서 그 절대좌표의 값이 벽에 닿는지 판단
         int cnt2=0;
          for(int j = 0; j<4 ;j++)
          {
              for(int k = 0; k<4;k++)
              {
                 int rotation2 = (rotation%4)+1 ; //1~4범위의 랜덤수 생성
                 if(rotation2 == 4)	//랜덤수가 4일 경우 0으로 지정하며 실질적으로 사용하는 수는 0~3이다.
                    rotation2 = 0;
                 if(blocks[random][rotation2][j][k] == 1)
                 {
                    curX[cnt2] = ((k*blocksize)+wid)/blocksize;
                    curY[cnt2] = ((j*blocksize)+hgt)/blocksize;
                    cnt2++;
                 }    
              }
          }
          
          // curX,Y에 저장된 좌표를 이용하여 충돌 검사
          int chk = 0;
          int blank = 0;
          
           // 왼쪽 벽          
           if(gameboard[curY[0]][curX[0]] == 1 || (random == 6 && gameboard[curY[2]][curX[2]] == 1) || (random == 1 && gameboard[curY[1]][curX[1]] ==1 ))
           {
           		chk = 1; // 만약 다음 회전한 도형의 위치가 벽과 겹친다면 chk=1로 표시함    
                         System.out.println("chk1, 회전한 도형의 위치가 왼쪽 벽과 겹칩니다.");	//이클립스 콘솔창으로 제대로 작동하는지 확인 가능
                         if(random == 3)// 일자막대(block[3][-][-][-])의 경우 회전할 여유가 있는 공백이 없으면 회전막음
                         { 
                            for(int i=1;i<5;i++)
                               if(gameboard[curY[0]][curX[0]+i] == 0)
                                  blank++;
                            if(blank < 4)
                               chk = 4;
                            
                              System.out.println(blank);
                         }
                         else// 그 외의 경우 회전할 여유가 없는 공백이 없으면 회전 막음
                         { 
                            for(int i=1; i<4;i++)
                               if(gameboard[curY[0]][curX[0]+i] == 0)
                                  blank++;
                            if(blank <3)
                               chk = 4;
                            System.out.println("blank2, 회전할 공간이 없습니다.");//이클립스 콘솔창으로 제대로 작동하는지 확인 가능
                            System.out.println(blank);
                         }
                         
                      }
            
          
             
            //오른쪽 벽
            else if(gameboard[curY[2]][curX[2]] == 1)
            {
                  chk = 2; // 만약 다음 회전한 도형의 위치가 벽과 겹친다면 chk=2로 표시함  
                       System.out.println("chk2");
                       
                       for(int i=1; i<5;i++)
                          if(gameboard[curY[2]][curX[2]-i] == 0)
                             blank ++;
                       if(blank < 4)
                          chk = 4;
                       System.out.println("blank2, 회전할 도형의 위치가 오른쪽 벽과 겹칩니다.");//이클립스 콘솔창으로 제대로 작동하는지 확인 가능
                       System.out.println(blank); 
             }
             else if(gameboard[curY[3]][curX[3]] == 1)
             {
                   chk = 3; // 만약 다음 회전한 도형의 위치가 벽과 겹친다면 chk=3로 표시함    
                       System.out.println("chk3, 회전할 도형의 위치가 오른쪽 벽과 겹칩니다");//이클립스 콘솔창으로 제대로 작동하는지 확인 가능
                       for(int i=0; i<5;i++)
                          if(gameboard[curY[3]][curX[3]-i] == 0)
                             blank ++;
                       if(blank < 4)
                    	   chk = 4;
                       System.out.println(blank);
             }
          
          if(chk == 1) // chk = 1(회전한 도형의 위치가 벽과 중복되면)면 wid(가로) +20 이동
          { 
             wid += blocksize;
             rotation++;
             rotation = rotation%4;
            }
          else if (chk ==2)	// chk = 2(회전한 도형의 위치가 벽과 중복되면)면 wid(가로) -40 이동
          {
               wid -= blocksize*2;
               rotation++;
               rotation = rotation%4;
            }
          else if (chk ==3)// chk = 3(회전한 도형의 위치가 벽과 중복되면)면 wid(가로)로 -20 이동
          {
               wid -= blocksize;
               rotation++;
               rotation = rotation%4;
            }
          else if(chk == 4)
          {
               System.out.println("ban");
            }
          else
          {
               	rotation++;
                rotation = rotation%4;
          }
      
          
      }
      
      public void makeBorder(Graphics g)	//맵
      {
    	  //g.setColor(Color.GRAY); 에서 수정
    	  g.setColor(Color.WHITE);
    	  
         //draw3DRect(int x, int y, int width, int height, boolean raised) : 좌표(x, y)에서 크기(width, height)만큼 raised에 따라 오목하게 또는 볼록하게 사각형을 그린다.
         //True:입체(볼록) False:입체(오목)
         
         /*
          * 21.06.16 맵크기 수정하고 Border도 사이즈 교체
          * 21.06.18 gameboard[0][-] 교체하면서 Border 사이즈 다시 교체
          * 
          * 기존 : 
          *     g.draw3DRect(28, 70, 5, 365,true); // 기둥
          *     g.draw3DRect(265, 70, 5, 365, true); // 기둥
          * 
          */
         g.draw3DRect(34, 70, 5, 430 , true); // 왼쪽기둥
         g.draw3DRect(260, 70, 5, 430, true); // 오른쪽기둥
         g.draw3DRect(15, 500, 270, 5, true); // 바닥
         g.draw3DRect(15, 65, 270, 5, true); // 천장
      }
      
      void down()	//아래쪽 방향키 눌렀을 때 실행
      {
         hgt += blocksize;	//블록크기만큼 아래로 내림
         TP.repaint();	//새로그림
      }
      void moveUp()
      {
    	  /*
    	   * 추가한 부분
    	   * 처음 블럭이 생성될 때 천장과 부딛히지 않는지 판단하는 collision_UP()추가
    	   */
         int sel = collision_UP();
         
         rotationCheck();
         if(sel == 0 && limit == false)	// if(limit == false)에서 수정
             repaint();//새로그림
      }
      void moveDown()	//아래쪽으로 움직였을 때의 화면
      {
         if(limit == false)
         {
            hgt += blocksize;
            TP.repaint();//새로그림
         }
      }
      void moveLeft()//왼쪽으로 움직였을 때의 화면
      {
         int sel = collision_LEFT();// sel이 1이면 충돌, 0이면 충돌X
         if(sel == 0 && limit == false)
         {
            wid -= blocksize;
            TP.repaint(); //새로그림
         }
      }
      void moveRight()	//오른쪽으로 움직였을 때의 화면
      {
         int sel = collision_RIGHT();// sel이 1이면 충돌, 0이면 충돌X
         if(sel == 0 && limit == false)
         { 
            wid += blocksize;
            TP.repaint(); //새로그림
         }
      }
      
      
      /*
       * 추가할 부분
       * 스페이스바 입력시 블록을 바닥에 바로 붙이도록 함(Hard Drop)
       * 
       * C언어에서 구현했을 때(참고)
       * switch(key)
       * {
             case SPACE: //스페이스키 눌렀을때 
                  space_key_on=1; //스페이스키 flag를 띄움 
                    while(crush_on==0) //바닥에 닿을때까지 이동시킴
                    {  
                        drop_block();
                        score+=level; // hard drop 보너스
                        gotoxy(STATUS_X_ADJ, STATUS_Y_SCORE);
                        printf("        %6d", score); //점수 표시  
                    }
                    break;
                    .
                    .
                    .
          }
       * 
       * 
       * 오류발생 21.06.13
       * while문을 사용하면 패널이 멈추고 더이상 진행을 하지 않음(그냥 정지된것같음)
       * 이클립스를 종료해도 계속 창이 떠있다가 한참뒤에 꺼지는 거 보면 while이 무한 반복되면서 오류가 생기는것음 
       * 
       * 
       * 오류발생 21.06.17
       * for문을 사용하면 아래로 빨리 내려갈 수 는 있는데(바로 내려가는건 X)
       * 만약 바닥을 두칸 띄운상태에서 스페이스바를 누르면 맵 밖으로 나가는 부분이 생김
       * 나간 부분은 지워지고 나가지 않은 부분만 0->1로 되어서 바닥에 고정됨
       * 
       * 오류발생 21.06.18
       * 이중 for문을 이용하여 0인 경우에만 blocksize를 계속 더해서 아래로 내려가게 한 다음
       * gameboard가 1인경우(블록인경우) 반복을 멈추는 것으로 소스코드를 작성했으나
       * 어제 작성한 for문과 똑같은 오류 발생
       * 
       */
      void moveHardDrop()
      {       
    	  for(int y=1; y<23;y++)	//0은 벽면이므로 1부터 시작. 23도 벽면이므로 22까지 진행
          {
             for(int x=1; x<13; x++)//0은 벽면이므로 1부터 시작. 13도 벽면이므로 12까지 진행
             {
                if(gameboard[y][x] == 1)	//게임보드가 1인경우(블록으로 채워진 경우)
                {
                	break;
                }
                hgt+=blocksize;
             }
          }
             
    	  /*
    	  while(true)
    	  {
    		  if(limit == false)
    		  {
    			  hgt+=blocksize;
    		  }
    		  else
    		  {
    			  break;
    		  }
    	  }*/
    	  
    	  /*for(int i=1; i<23; i++)
    	  {
    		  for(int j=1; j<12; j++)
    		  {
    			  	if(gameboard[i][j])
    		  }
    			  hgt+=1;
    	  }*/
    	  TP.repaint();	//새로그림
      }
   }
   
   class TetrisThread extends Thread
   {
      TetrisPanel TP = new TetrisPanel();
      public void run()
      {
    	  /*
    	   * 추가한 부분
    	   * 점수에 따라 블록이 떨어지는 속도가 빨라지도록 수정 
    	   * 
    	   * 기본 속도 1.3초
    	   * 200점이상 800점 미만 1.0초
    	   * 800점이상 3000점 미만 0.65초
    	   * 그 이상 0.3초 
    	   */
         while(true)
         {
            try{
            	if((score*100) < 200) //초반 속도
            	{
            		sleep(1300);
            		if(limit == false) // limit이 false일 경우에만 작동. true가 되면 테트리스 작동중지
                        TP.down();
            	}
            	else if((score*100)>=200 && (score*100) < 800)
            	{
            		sleep(1000);
            		if(limit == false) // limit이 false일 경우에만 작동. true가 되면 테트리스 작동중지
                        TP.down();
            	}
            	else if((score*100)>=800 && (score*100) < 3000)
            	{
            		sleep(650);
            		if(limit == false) // limit이 false일 경우에만 작동. true가 되면 테트리스 작동중지
                        TP.down();
            	}
            	else	//3000점 이상
            	{
            		sleep(300);
            		if(limit == false) // limit이 false일 경우에만 작동. true가 되면 테트리스 작동중지
                        TP.down();
            	}
               
            }catch(InterruptedException e){
               return;
            }
            
         }
      }
 }
}
