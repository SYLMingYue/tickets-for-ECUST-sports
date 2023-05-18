# tickets-for-ECUST-sports

_本仓库将记录我通过chatgpt学习编写自动化脚本来预定学校羽毛球馆的历程，仅供学习，若有侵权请联系我删除。若需模仿验证，请保证你已经安装了较高版本python坏境。_

## 1下载使用WebDriver
WebDriver是一个用于自动化浏览器操作的工具。它提供了一个编程接口，可以通过代码来模拟用户与浏览器的交互行为，例如点击按钮、填写表单、导航到不同的网页等操作。需要注意的是，不同的浏览器需要下载WebDriver中不同的驱动程序，以我使用的chrome版本为113.0.5672.127为例，前往WebDriver的chromeDriver[下载地址](https://sites.google.com/chromium.org/driver/?pli=1)，选择对应的chromeDriver版本并下载解压，

## 2使用pip安装Selenium库
当涉及到网页自动化和浏览器控制时，[Selenium](https://www.selenium.dev/documentation/)是一个广泛使用的Python库。它提供了一组丰富的功能，用于模拟用户与网页的交互，包括点击按钮、填写表单、获取元素、处理弹窗等。pip是Python的包管理工具，它用于安装和管理Python库。如果你的Python版本是3.4或更高版本，则pip已经随Python安装在内。你可以在终端或命令提示符中运行以下命令来检查pip版本。在系统中配置好python以及pip的情况下，在cmd下输入 `pip install selenium` 即可安装Selenium。安装完成后，可以使用以下命令验证是否成功安装了Selenium库：`pip show selenium` 。

## 3使用VSC来编写代码自动化控制chrome浏览器

### 3.1 准备工作
导入需要的库
```
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver import ActionChains
import time

# 设置浏览器选项（例如Chrome）
options = webdriver.ChromeOptions()
options.add_argument('--auto-open-devtools-for-tabs')
# 设置ChromeDriver的路径(双引号内填ChromeDriver的路径)
chromedriver_path = "D:\BaiduNetdiskDownload\WebDriver\chromedriver.exe"
# 初始化WebDriver
driver = webdriver.Chrome(executable_path=chromedriver_path)
driver = webdriver.Chrome(options=options)
# 配置选项，使浏览器在后台运行，无界面显示
# options.add_argument('--headless')
# options.add_argument('--disable-gpu')
```
### 3.2预定
*说明：在chrome中选择元素elememt时，最简单的方式是ID以及XPATH方法，查看ID以及XPATH的方式为在开发者模式中选中元素即可查看或者copy，另外，可能是学校的预定网站设置了防火墙，我发现在普通模式（非开发者模式）下无法显示页面的全部内容，所以打开开发者模式是必须的。*
```
# 打开目标网页
driver.get('https://szcg.ecust.edu.cn/wx/#/ticketIndex')
button_element = driver.find_element(By.LINK_TEXT, '校园统一认证')
button_element.click()

# 定位账号输入框并输入账号
username_input = driver.find_element(By.ID, 'username')
username_input.send_keys('此处填写你的学号')

# 定位密码输入框并输入密码
password_input = driver.find_element(By.ID, 'password')
password_input.send_keys('此处填写你的密码')

# 提交表单
submit_button = driver.find_element(By.XPATH, '//*[@id="casLoginForm"]/p[5]/button')
submit_button.click()

# 选择羽毛球并预定
badminton_button = WebDriverWait(driver, 10).until(EC.visibility_of_element_located((By.XPATH,'//*[@id="app"]/div/div[5]/div[2]/div[1]/div/ul/li[3]')))
badminton_button.click()

xuhuibadminton_button = WebDriverWait(driver, 10).until(EC.visibility_of_element_located((By.XPATH,'//*[@id="app"]/div/div[5]/div[2]/div[2]/div/div[1]/ul/li/a/div/div/p/span')))
xuhuibadminton_button.click()

schedule_tomorrow = WebDriverWait(driver, 10).until(EC.visibility_of_element_located((By.XPATH,'//*[@id="app"]/div/div[5]/div[3]/div[2]/div/div[2]/div[2]/div[2]')))
schedule_tomorrow.click()

未完待续
```


## 学习与参考
[^1]chatgpt

[^2]https://zhuanlan.zhihu.com/p/111859925

[^3]https://www.selenium.dev/documentation/webdriver/elements/locators/
