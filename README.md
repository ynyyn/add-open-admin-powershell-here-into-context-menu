# add-open-admin-powershell-here-into-context-menu

Registry script: Add open PowerShell window here as administrator in context menu

注册表脚本分享：在右键菜单中添加在此处打开管理员 PowerShell 窗口

---

Basically tweaking under `HKEY_CLASSES_ROOT\Directory\Background\shell\runas` (initially not exists).

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\Directory\Background\shell\runas]
@="@shell32.dll,-37448"
"Extended"=""
"HasLUAShield"=""
"NoWorkingDirectory"=""
"ShowBasedOnVelocityId"=dword:00639bc8

[HKEY_CLASSES_ROOT\Directory\Background\shell\runas\command]
@="powershell.exe -noexit -command Set-Location -literalPath '%V'"

```

This will add a new item/entry into the context menu of <kbd>Shift</kbd>+<kbd>Right Click</kbd> on directory background, offering a functionality to *Open PowerShell window here as administrator*.

It models after the "built-in" *Open PowerShell window here* item implementation `HKEY_CLASSES_ROOT\Directory\Background\shell\Powershell` with minor adaptions.

### Explanation
#### `@="@shell32.dll,-37448"`?

It controls the title of the item in context menu. `@shell32.dll,-37448` is a resource reference notation (for localization), pointing to a UI text, making this item displayed in your system language (follow your locale preference). I pick it after thoroughly examining all available UI text in shell32.dll. (It is officially referred in the ribbon menu of the explorer.)

TODO...
