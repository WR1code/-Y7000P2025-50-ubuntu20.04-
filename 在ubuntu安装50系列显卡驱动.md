最快的方法，避免纯命令行，直接使用自带的软件与更新
<img width="817" height="589" alt="image" src="https://github.com/user-attachments/assets/8735e0dc-cb8c-4632-a562-a26b00297413" />
如果你发现自己的附加驱动是空的，在其他软件选项处选择添加并更新你的驱动源
http://ppa.launchpad.net/graphics-drivers/ppa/ubuntu

我是拯救者Y7000P2025版本，我选择的是图片中的open驱动，不带open标签的570经测试无法兼容
如果你要查看你的笔记本的显卡型号

lspci | grep -i vga

如果你要确定显卡是否安装成功（英伟达）

nvidia-smi

<img width="824" height="72" alt="image" src="https://github.com/user-attachments/assets/f9746b37-1cf1-48a9-9fa4-576cd18aa23a" />

如果出不来，跑模型的时候大概率是用不了GPU加速的，也无法连接分显示屏
