# Vite Heroku Deploy
實驗，vite React app 在 Heroku 做 static deploy。

- Heroku 可支持[靜態部署](https://blog.heroku.com/deploying-react-with-zero-configuration)，目前可以直接對應 [Create-React-App](https://create-react-app.dev/docs/deployment#heroku)
- Heroku 靜態部署需設定 [BuildPack](https://devcenter.heroku.com/articles/buildpacks)
- React CRA 有專門的 BuildPack [create-react-app-buildpack](https://github.com/mars/create-react-app-buildpack)
- Vite 目前官方文件說明，使用的是靜態網站公版的 [
heroku-buildpack-static](https://github.com/heroku/heroku-buildpack-static)
- heroku-buildpack-static 設定上不會進行 build 動作，所以 Vite app 需要比照 gh-pages 的方式，在本機 build 後，把 dist 包也上傳到 Heroku 才行

## 部署方案
這邊實驗性做了兩個方案，並用 .sh file 做自動化處理：
- `/deploy-gh.sh`，比照 gh-pages 將 build 包作為獨立新 branch push 至 github，Heorku 設定連線此 branch 進行部署
- `/deploy-heroku.sh`，將 build 包作為獨立新 branch，直接 push 至 Heroku。
  - 有坑，windows 執行 .sh file 時，執行 `heroku git:remote [target]` 會直接中斷掉，所以不設定 remote，直接對 heroku 的 repo 進行 push。
