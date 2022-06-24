## describe

- The best screenshot tool in Linux !
- Support for gui 
- Support for command

## install

Using command as follwing to install flameshot in **ubuntu**

```bash
sudo apt install flameshot
```

## configuration

After installation, next step is **configuration** because it **cannot supoort shortcut within software**, but we can use **system shortcut** to implement this idea.

Open **settings** in gui ，select the **Keyboard Shortcuts** chocie as picture show.

![keboard-shortcuts | 600](additions/keyboard-shortcut-1.png)

Add new shortcut , name as you think, but command should be `flameshot gui` . 

![](additions/keyboard-shortcut-2.png)

There have other **command** selections for you to use, but the `flameshot gui` is sufficient to use.

```bash
# open capture window
flameshot gui

# openc capyure window and set store location
flameshot gui -p /path/to/capture

# open configuration window
# flameshot config
```

