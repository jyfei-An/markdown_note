# qss教程

https://doc.qt.io/qt-5/stylesheet.html



# qInstallFrameWork

## 使用方法

windows

```
..\..\bin\binarycreator.exe -c config\config.xml -p packages YourInstaller.exe
```

linux

```
/home/jiayunfe/Qt/QtIFW-3.2.2/bin/binarycreator -c config/config.xml -p packages 12YSim0.1.19.run
```



## windows下exe增加桌面快捷方式

```cpp
Component.prototype.createOperations = function()
{
    try {
        // call the base create operations function
        component.createOperations();
        if (installer.value("os") == "win") { 
            try {
                var userProfile = installer.environmentVariable("USERPROFILE");
                installer.setValue("UserProfile", userProfile);
                component.addOperation("CreateShortcut", "@TargetDir@\\MiamPlayer.exe", "@UserProfile@\\Desktop\\MiamPlayer.lnk");
            } catch (e) {
                // Do nothing if key doesn't exist
            }
        }
    } catch (e) {
        print(e);
    }
}
```



# qt翻译

无法翻译自带的messagebox等控件，可参考下面github链接

https://github.com/wisaly/qtbase_zh



# 获取发送信号物体

```
 QObject *object = QObject::sender();
 QLineEdit *psenderlineedit = static_cast<QLineEdit*>(object);
```



# QLayout

![image-20200515221802526](C:\Users\jiayunfei\AppData\Roaming\Typora\typora-user-images\image-20200515221802526.png)



# QDir的使用

## 1 判断文件夹是否存在

```
QString dir_str = "E:\CodeTest";

// 检查目录是否存在，若不存在则新建
QDir dir;
if (!dir.exists(dir_str))
{
bool res = dir.mkpath(dir_str);
qDebug() << "新建目录是否成功" << res;
}
```



# QPushButton的使用

## 信号槽函数

```
 connect(ui.ok_btn_, &QPushButton::clicked, this, &CSAddSubModel::accept);
 connect(ui.cancel_btn_, &QPushButton::clicked, this, &QDialog::reject);
```

# QDialog的使用

## 1 去掉问号按钮

下面两种方法均可让对话框的问号按钮去掉，如果其中一种不生效，可更换另一种

1 方法一

```
Qt::WindowFlags flags = Qt::Dialog;
flags |= Qt::WindowCloseButtonHint;
dlg->setWindowFlags(flags);
```

2 方法二

```
this->setWindowFlags(Qt::CustomizeWindowHint | Qt::WindowCloseButtonHint);
```

##  2 使最大化按钮失效

```
setWindowFlags(Qt::WindowCloseButtonHint|Qt::WindowMinimizeButtonHint);
```

##  3 初始界面最大化

```
setWindowState(Qt::WindowMaximized);
```



# QTableWidget的使用

## 1 设置某列不可编辑

```
QTableWidgetItem *item = new QTableWidgetItem("test");
item->setFlags(item->flags() & (~Qt::ItemIsEditable));
```

## 2 设置表格禁止编辑

```
ui.tablewidget->setEditTriggers(QAbstractItemView::NoEditTriggers);
```

## 3 设置单击选择某一行

不是选择某一项

```
//设置单击选择一行
ui.tablewidget->setSelectionBehavior(QAbstractItemView::SelectRows);
//设置只能选择一行，不能多行选中
ui.tablewidget->setSelectionMode(QAbstractItemView::SingleSelection);
```

##  4 设置表格列宽

设置表格最后一列自适应拉伸

```
ui.tablewidget->setColumnWidth(0, 220);
ui.tablewidget->setColumnWidth(1, 65);
ui.tablewidget->horizontalHeader()->setStretchLastSection(true);
```

##  5 表格插入数据

```
int row_count = ui.tablewidget->rowCount();
ui.tablewidget->insertRow(row_count);
QTableWidgetItem *item_time = new QTableWidgetItem(current_date);
QTableWidgetItem *item_level = new QTableWidgetItem(QString::fromStdString(level));
QTableWidgetItem *item_data = new QTableWidgetItem(QString::fromStdString(data));
ui.tablewidget->setItem(row_count, 0, item_time);
ui.tablewidget->setItem(row_count, 1, item_level);
ui.tablewidget->setItem(row_count, 2, item_data);
```

##  6 删除表格的所有行

```
ui.table_widget_->clearContents();
for (int i = ui.log_widget_->rowCount(); i > 0; i--)
{
    ui.log_widget_->removeRow(0);
}
```

## 7 设置表格自适应拉伸（均分表格）

表格可以随着窗口的变大而变大

```
 ui.tableWidget->horizontalHeader()->setSectionResizeMode(
    QHeaderView::Stretch);
 ui.tableWidget->verticalHeader()->setSectionResizeMode(
    QHeaderView::Stretch);
```

## 8 设置表格的字体颜色和背景颜色

```
newItem = QTableWidgetItem("测试")  
newItem.setBackgroundColor(QColor(0,60,10))  
newItem.setTextColor(QColor(200,111,100))          
self.MyTable.setItem(0, 0, newItem)  
```

## 9 移除当前选中行

```
int currow = ui.topics_table_->currentRow();
if (currow == -1) {
    return;
}
ui.topics_table_->removeRow(currow);
```



# QTreewidget的使用

##  QtreeWidget显示右键菜单

```
#include "treewidget.h"

#include <QPushButton>
#include <QMenu>

TreeWidget::TreeWidget(QWidget *parent)
  : QMainWindow(parent)
{
  ui.setupUi(this);

  //设置树形控件每一列的名称
  QStringList sl;
  sl << u8"名称";
  ui.treeWidget->setHeaderLabels(sl);

  //treewidget鼠标右键菜单事件，需要在代码手动设置ContextMenuPolicy属性或者在ui文件中设置
  ui.treeWidget->setContextMenuPolicy(Qt::CustomContextMenu);
  connect(ui.treeWidget, &QWidget::customContextMenuRequested, this,
          &TreeWidget::ShowContextMenu);

  //为树形控件添加一级结点
  connect(ui.add_first_node_button, &QPushButton::clicked, this,
          &TreeWidget::AddFirstNode);

  //为树形控件添加二级结点
  connect(ui.add_second_node_button, &QPushButton::clicked, this,
          &TreeWidget::AddSecondNode);
}

void TreeWidget::ShowContextMenu(const QPoint &pos)
{
  QMenu *menu = new QMenu(this);
  QTreeWidgetItem *item = ui.treeWidget->itemAt(pos);
  if (item)
  {
    if ((int)TreeItemType::kFisrtNode == item->type())
    {
      QAction *action1 = new QAction(u8"一级结点1", this);
      menu->addAction(action1);
      QAction *action2 = new QAction(u8"一级结点2", this);
      menu->addAction(action2);
      QAction *action3 = new QAction(u8"一级结点3", this);
      menu->addAction(action3);
    }
    else if ((int)TreeItemType::kSecondNode == item->type())
    {
      QAction *action1 = new QAction(u8"二级结点1", this);
      menu->addAction(action1);
      QAction *action2 = new QAction(u8"二级结点2", this);
      menu->addAction(action2);
      QAction *action3 = new QAction(u8"二级结点3", this);
      menu->addAction(action3);
    }
  }
  else
  { //在空白处点击，没有选中QTreeWidgetItem
    QAction *action1 = new QAction(u8"空白结点1", this);
    menu->addAction(action1);
    QAction *action2 = new QAction(u8"空白结点2", this);
    menu->addAction(action2);
    QAction *action3 = new QAction(u8"空白结点3", this);
    menu->addAction(action3);
  }

  menu->exec(QCursor::pos());
}
```

## QtreeWidget添加结点

```
void TreeWidget::AddFirstNode()
{
  QTreeWidgetItem *node = new QTreeWidgetItem(ui.treeWidget,
      (int)TreeItemType::kFisrtNode);
  QString text = QString::number(++node_sequence_);
  node->setText(0, text);
  ui.treeWidget->addTopLevelItem(node);
}

void TreeWidget::AddSecondNode()
{
  QTreeWidgetItem *it = ui.treeWidget->currentItem();
  if (!it)
  {
    return;
  }
  QTreeWidgetItem *item = new QTreeWidgetItem(it, (int)TreeItemType::kSecondNode);
  item->setText(0,u8"二级结点");
  it->addChild(item);
}
```

## QtreeWidget删除结点

```
void TreeWidget::DeleteNode()
{
  QTreeWidgetItem *item = ui.treeWidget->currentItem();
  if (!item)
  {
    return;
  }
  if ((int)TreeItemType::kFisrtNode == item->type())
  {
    int index = ui.treeWidget->indexOfTopLevelItem(item);
    ui.treeWidget->takeTopLevelItem(index);
  }
  else if ((int)TreeItemType::kSecondNode == item->type())
  {
    ui.treeWidget->removeItemWidget(item, 0);
    delete item;
  }
}
```

![img](https://img2018.cnblogs.com/blog/1317399/201909/1317399-20190904105318609-2017294857.png)

# linux安装Qt

## Install Qt Creator

```bash
sudo apt install build-essential
sudo apt install qtcreator
```

If you want Qt 5 to be the default Qt version to be used when using development binaries like qmake, install the following package:

```bash
sudo apt install qt5-default
```

## Install documentation and examples

If Qt Creator is installed thanks to the Ubuntu Sofware Center or thanks to the synaptic package manager, documentation for Qt Creator is not installed. Hitting the F1 key will show you the following message : **“No documentation available”**. This can easily be solved by installing the Qt documentation:

```bash
sudo apt install qt5-doc
```

And eventually:

```bash
sudo apt install qt5-doc-html qtbase5-doc-html
```

If examples are still missing:

```bash
sudo apt install qtbase5-examples
```

## install svg,charts

```
sudo apt install libqt5svg5-dev
sudo apt-get install qttools5-dev
sudo apt install libqt5charts5-dev
```

