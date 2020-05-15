# 获取发送信号物体

```
 QObject *object = QObject::sender();
 QLineEdit *psenderlineedit = static_cast<QLineEdit*>(object);
```



# QLayout

![image-20200515221802526](C:\Users\jiayunfei\AppData\Roaming\Typora\typora-user-images\image-20200515221802526.png)

# QPushButton的使用

## 信号槽函数

```
 connect(ui.ok_btn_, &QPushButton::clicked, this, &CSAddSubModel::accept);
 connect(ui.cancel_btn_, &QPushButton::clicked, this, &QDialog::reject);
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

