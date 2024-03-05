# Mac

## 設定

```
## .DS_Store ファイル作成を無効化
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
defaults write com.apple.desktopservices DSDontWriteUSBStores -bool true

# Mouse
## カーソルスピードを最大化
defaults write -g com.apple.mouse.scaling 3
## スワイプスクロールを無効化(スクロールを反転させる)
defaults write -g com.apple.swipescrolldirection -bool false

# Keyboard
## キー押下時のホールドを無効化(キーリピートを効くようにする)
defaults write -g ApplePressAndHoldEnabled -bool false

# Finder
## 拡張子まで表示
defaults write NSGlobalDomain AppleShowAllExtensions -bool true
## 隠しファイルを表示
defaults write com.apple.Finder AppleShowAllFiles -bool true
## パスバーを表示
defaults write com.apple.finder ShowPathbar -bool true
```

`ioreg -p IOUSB -c IOUSBDevice | grep -e class -e idVendor -e id`

```
## CtrlとCommandを入れ替え
keyboard_id="6127-24814-0"
defaults -currentHost write -g com.apple.keyboard.modifiermapping.${keyboard_id} -array-add "
<dict>
  <key>HIDKeyboardModifierMappingDst</key>\
  <integer>30064771296</integer>\
  <key>HIDKeyboardModifierMappingSrc</key>\
  <integer>30064771299</integer>\
</dict>
"
defaults -currentHost write -g com.apple.keyboard.modifiermapping.${keyboard_id} -array-add "
<dict>
  <key>HIDKeyboardModifierMappingDst</key>\
  <integer>30064771299</integer>\
  <key>HIDKeyboardModifierMappingSrc</key>\
  <integer>30064771296</integer>\
</dict>
"
```