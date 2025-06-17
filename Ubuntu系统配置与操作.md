# Ubuntu系统相关操作

## 0. Ubuntu系统软件列表
	1. Obsidian
	2. Onenote
	3. Syncthing
	4. 坚果云
	5. Zetoro
	6. Vscode
	7. Google chrome
	8. Send local
	9. Tweaks
	10. Catfish:搜索软件
	11. Flameshot截图软件
	12. Htop
	13. Inscape
	14. NoMachine
	15. OBS Studio
	16. Redshift
	17. TeXstudio
	18. Ubuntu Cleaner
	19. Kaly Software store
	20. Termius
	21. WPS
  22. Xmind

## 1. ubuntu添加环境变量
例如，将ollama增加高并发能力。
```shell
sudo vim /etc/environment

OLLAMA_MAX_LOADED_MODELS=4
OLLAMA_NUM_PARALLEL=4
```
