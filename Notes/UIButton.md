# UIButton

### Button Types

	typedef enum {
		UIButtonTypeCustom = 0,//自定义类型
		UIButtonTypeSystem,//类似导航栏和工具栏的系统按钮样式,若使用此样式，在使用setImage时会显示异常
		UIButtonTypeDetailDisclosure,
		UIButtonTypeInfoLight,
		UIButtonTypeInfoDark,//圆圈加i
		UIButtonTypeContactAdd,//圆圈加+
		UIButtonTypeRoundedRect,//舍弃 用system代替
	} UIButtonType;


	
### Creating Buttons

	UIButton *btn1 = [UIButton buttonWithType:UIButtonType*];
	UIButton *btn2 = [[UIButon alloc] initWithFrame:CGRectMake(x,x,x,x)];

### Button's titleLabel

	@property(nonatomic, readonly, retain) UILabel *titleLabel	

> 虽然titleLabel是只读的，但是他自己的属性是可读写的(font,lineBreakMode)。
> 
> 不要使用 ` .语法`来设置label的text、textcolor、textshadowcolor，要用setTitle* forState

   state :

	UIControlStateNormal                //常规状态显现 
	UIControlStateHighlighted           //高亮状态显现(被按下去时)
	UIControlStateDisabled              //禁用的状态才会显现
	UIControlStateSelected              //选中状态
	UIControlStateApplication            //当应用程序标志时 
	UIControlStateReserved              //为内部框架预留，可以不管他 
-

	//返回在某个状态下，按钮标题的富文本
	- (NSAttributedString *)attributedTitleForState:(UIControlState)state
		
	//返回按钮在某个状态下的标题颜色
	- (UIColor *)titleColorForState:(UIControlState)state
		
	//设置某个状态下按钮标题的阴影颜色
	- (void)setTitleShadowColor:(UIColor *)color
	                   forState:(UIControlState)state
	                   
	//标题的阴影改变时，按钮是否高亮显示。默认为NO
	@property(nonatomic) BOOL reversesTitleShadowWhenHighlighted
	
### Button's Presentation

	//按钮高亮的情况下，图像的颜色是否要加深一点。默认是YES，(是否有高亮状态)
	@property(nonatomic) BOOL adjustsImageWhenHighlighted	
	
	//按钮禁用的情况下，图像的颜色是否要加深一点。默认是YES
	@property(nonatomic) BOOL adjustsImageWhenDisabled
	
	//按下按钮是否会发光。默认是NO
	@property(nonatomic) BOOL showsTouchWhenHighlighted
	
	//设置按钮的背景图片(图片被拉伸)
	- (void)setBackgroundImage:(UIImage *)image forState:(UIControlState)state
	//设置按钮的背景图片(保持原大小)
	- (void)setBackgroundImage:(UIImage *)image forState:(UIControlState)state
      
### Button's Edge Inset

	//设置按钮的内部内容（包含按钮图片和标题）离按钮边缘上下左右的距离。
	@property(nonatomic) UIEdgeInsets contentEdgeInsets
	
	//设置按钮的内部标题离按钮边缘上下左右的距离
	@property(nonatomic) UIEdgeInsets titleEdgeInsets
	
	//设置按钮的内部图片离按钮边缘上下左右的距离
	@property(nonatomic) UIEdgeInsets imageEdgeInsets
	
eg.

	UIEdgeInsets insets;    // 设置间距
	insets.top = insets.bottom = insets.right = insets.left = 10;
	btn.contentEdgeInsets = insets;//按钮按钮内部
	btn.contentEdgeInsets = insets;//标题间距
	btn.contentEdgeInsets = insets;//图片间距
	
### Get Button's State

	//获取按钮状态，只读属性
	@property(nonatomic, readonly) UIButtonType buttonType
	
	//获取按钮当前标题，只读属性
	@property(nonatomic, readonly, retain) NSString *currentTitle
	
	//获取按钮当前的富文本标题
	@property(nonatomic, readonly, retain) NSAttributedString *currentAttributedTitle
	
	//获取当前标题的颜色
	@property(nonatomic, readonly, retain) UIColor *currentTitleColor
	
	//获取当前标题的阴影颜色
	@property(nonatomic, readonly, retain) UIColor *currentTitleShadowColor
	
	//获取当前按钮的图片
	@property(nonatomic, readonly, retain) UIImage *currentImage
	
	//获取当前按钮的背景图片
	@property(nonatomic, readonly, retain) UIImage *currentBackgroundImage
	
	//获取当前按钮的图片框对象
	@property(nonatomic, readonly, retain) UIImageView *imageView
    
### Button's Events

//给按钮添加点击事件
[button addTarget:self action:@selector(action:) forControlEvents:UIControlEventTouchUpInside];

	UIControlEventTouchDown                 // 单点触摸按下事件：用户点触屏幕，或者又有新手指落下的时候。
	UIControlEventTouchDownRepeat       // 多点触摸按下事件，点触计数大于1：用户按下第二、三、或第四根手指的时候。
	UIControlEventTouchDragInside       // 当一次触摸在控件窗口内拖动时。
	UIControlEventTouchDragOutside      // 当一次触摸在控件窗口之外拖动时。
	UIControlEventTouchDragEnter        // 当一次触摸从控件窗口之外拖动到内部时
	UIControlEventTouchDragExit         // 当一次触摸从控件窗口内部拖动到外部时。
	UIControlEventTouchUpInside         // 所有在控件之内触摸抬起事件
	UIControlEventTouchUpOutside        // 所有在控件之外触摸抬起事件(点触必须开始与控件内部才会发送通知)。
	UIControlEventTouchCancel           //所有触摸取消事件，即一次触摸因为放上了太多手指而被取消，或者被上锁或者电话呼叫打断。
	UIControlEventValueChanged          // 当控件的值发生改变时，发送通知。用于滑块、分段控件、以及其他取值的控件。你可以配置滑块控件何时发送通知，在滑块被放下时发送，或者在被拖动时发送。
	UIControlEventEditingDidBegin       // 当文本控件中开始编辑时发送通知
	UIControlEventEditingChanged        // 当文本控件中的文本被改变时发送通知。
    UIControlEventEditingDidEnd         // 当文本控件中编辑结束时发送通知。
    UIControlEventEditingDidEndOnExit   // 当文本控件内通过按下回车键（或等价行为）结束编辑时，发送通知。
	UIControlEventAllTouchEvents        // 通知所有触摸事件。
    UIControlEventAllEditingEvents      // 通知所有关于文本编辑的事件。
    UIControlEventApplicationReserved   // range available for application use
    UIControlEventSystemReserved        // range reserved for internal framework use
    UIControlEventAllEvents             // 通知所有事件
    
 常按事件
 
 	//长按按钮
    UILongPressGestureRecognizer *longPress = [[UILongPressGestureRecognizer alloc]initWithTarget:self action:@selector(btnLongPressedWithButton)];
    //    longPress.minimumPressDuration = 0.5;    //最短按压时间,一般地，此句不写也可以
    [btn1 addGestureRecognizer:longPress];