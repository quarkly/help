---
id: integration-with-paypal
title: Integration with PayPal
sidebar_label: Integration with PayPal
---


Для примера создадим сайт для продажи нескольких товаров с использованием PayPal.

## 1. Контент сайта

Создаем новый пустой проект в Quarkly.

### 1.1 Создаем Главную страницу

Копируем код ниже, и вставляем его в нашу страницу.

```jsx
<Section padding="80px 0 80px 0">
	<Override slot="SectionContent" flex-direction="row" flex-wrap="wrap" />
	<Box
		display="flex"
		align-items="center"
		flex-direction="column"
		justify-content="center"
		margin="0px 0px 64px 0px"
		width="100%"
		sm-margin="0px 0px 30px 0px"
		padding="0px 200px 0px 200px"
		lg-padding="0px 0px 0px 0px"
	>
		<Text margin="0px 0px 16px 0px" font="--headline1" text-align="center" sm-font="normal 700 42px/1.2 &quot;Source Sans Pro&quot;, sans-serif">
			Products
		</Text>
		<Text margin="0px 0px 0px 0px" color="--darkL2" text-align="center" font="--lead">
			Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua
		</Text>
	</Box>
	<Box
		display="grid"
		flex-wrap="wrap"
		width="100%"
		align-items="center"
		justify-content="center"
		grid-template-columns="repeat(3, 1fr)"
		grid-gap="30px"
		md-grid-template-columns="1fr"
	>
		<Box
			width="100%"
			display="flex"
			padding="7px 7px 40px 7px"
			border-radius="24px"
			align-items="center"
			flex-direction="column"
			border-width="1px"
			border-style="solid"
			border-color="--color-lightD2"
			justify-content="center"
		>
			<Image
				src="https://images.unsplash.com/photo-1618354691229-88d47f285158?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=715&q=80"
				border-radius="16px"
				margin="0px 0px 32px 0px"
				max-width="100%"
				md-width="100%"
				width="100%"
				height="278px"
				object-fit="cover"
			/>
			<Box
				display="flex"
				flex-direction="column"
				padding="0px 30px 0px 30px"
				align-items="flex-start"
				justify-content="flex-start"
			>
				<Text margin="0px 0px 8px 0px" font="--headline3">
					Long Sleeve

				</Text>
				<Text margin="0px 0px 16px 0px" text-align="center" font="--lead">
					$25.00
				</Text>
				<Link
					href="/long-sleeve#"
					text-decoration-line="initial"
					color="--dark"
					font="--lead"
					padding="12px 24px 12px 24px"
					border-radius="8px"
					background="--color-secondary"
					lg-padding="12px 20px 12px 20px"
					transition="background-color 0.2s ease-in-out 0s"
					hover-transition="background-color 0.2s ease-in-out 0s"
					hover-background="--color-orange"
				>
					Read more
				</Link>
			</Box>
		</Box>
		<Box
			width="100%"
			display="flex"
			padding="7px 7px 40px 7px"
			border-radius="24px"
			align-items="center"
			flex-direction="column"
			border-width="1px"
			border-style="solid"
			border-color="--color-lightD2"
			justify-content="center"
			position="relative"
		>
			<Image
				src="https://images.unsplash.com/photo-1618354691373-d851c5c3a990?ixlib=rb-1.2.1&q=85&fm=jpg&crop=entropy&cs=srgb&h=2000"
				border-radius="16px"
				max-width="100%"
				md-width="100%"
				max-height="278px"
				object-fit="cover"
				width="100%"
				margin="0px 0px 32px 0px"
			/>
			<Box
				display="flex"
				flex-direction="column"
				padding="0px 30px 0px 30px"
				align-items="flex-start"
				justify-content="flex-start"
			>
				<Text margin="0px 0px 8px 0px" font="--headline3">
					T-shirt Small Logo
				</Text>
				<Text margin="0px 0px 16px 0px" text-align="center" font="--lead">
					$22.00
				</Text>
				<Link
					href="/t-shirt-small-logo#"
					text-decoration-line="initial"
					color="--dark"
					font="--lead"
					padding="12px 24px 12px 24px"
					border-radius="8px"
					background="--color-secondary"
					lg-padding="12px 20px 12px 20px"
					transition="background-color 0.2s ease-in-out 0s"
					hover-transition="background-color 0.2s ease-in-out 0s"
					hover-background="--color-orange"
				>
					Read more
				</Link>
			</Box>
		</Box>
		<Box
			width="100%"
			display="flex"
			padding="7px 7px 40px 7px"
			border-radius="24px"
			align-items="center"
			flex-direction="column"
			border-width="1px"
			border-style="solid"
			border-color="--color-lightD2"
			justify-content="center"
		>
			<Image
				src="https://images.unsplash.com/photo-1618354691438-25bc04584c23?ixlib=rb-1.2.1&q=85&fm=jpg&crop=entropy&cs=srgb&h=2000"
				border-radius="16px"
				margin="0px 0px 32px 0px"
				max-width="100%"
				md-width="100%"
				max-height="278px"
				object-fit="cover"
				width="100%"
			/>
			<Box
				display="flex"
				flex-direction="column"
				padding="0px 30px 0px 30px"
				align-items="flex-start"
				justify-content="flex-start"
			>
				<Text margin="0px 0px 8px 0px" font="--headline3">
					T-shirt Big Logo
				</Text>
				<Text margin="0px 0px 16px 0px" text-align="center" font="--lead">
					$23.00
				</Text>
				<Link
					href="/t-shirt-big-logo#"
					text-decoration-line="initial"
					color="--dark"
					font="--lead"
					padding="12px 24px 12px 24px"
					border-radius="8px"
					background="--color-secondary"
					lg-padding="12px 20px 12px 20px"
					transition="background-color 0.2s ease-in-out 0s"
					hover-transition="background-color 0.2s ease-in-out 0s"
					hover-background="--color-orange"
				>
					Read more
				</Link>
			</Box>
		</Box>
	</Box>
</Section>
```

Получаем вот такой результат:

![Site preview](/scr/tutorials/integration-with-paypal-site-preview.png)

### 1.2 Компонент оплаты

Создаем компонент с названием QuarklyPayPal.

```jsx
import React from 'react';
import atomize from "@quarkly/atomize";
import { Box } from "@quarkly/widgets"
import { PayPalButton } from "react-paypal-button-v2";

const QuarklyPaypalButton = ({ clientId, amount, itemName, currencyCode, itemDescription, ...props }) => {
  return <Box {...props}>
    <PayPalButton
      currency={currencyCode}
      // onSuccess вызывается при успешном совершении транзакции
      // Здесь можно отправить запрос, чтобы сохранить эту транзакцию
      onSuccess={(details, data) => {
        const transactionId = details.purchase_units[0].payments.captures[0].id;
        
        alert(`Transaction completed by ${details.payer.name.given_name}\nYour transaction id: ${transactionId}`);
      }}
      // Подробнее о createOrder:
      // https://developer.paypal.com/sdk/js/reference/#createorder
      createOrder={(data, actions) => {
        return actions.order.create({
          purchase_units: [{
            amount: {
              currency_code: currencyCode,
              value: amount,
              breakdown: {
                item_total: {
                  currency_code: currencyCode,
                  value: amount
                }
              }
            },
            items: [{
              name: itemName,
              description: itemDescription,
              unit_amount: {
                currency_code: currencyCode,
                value: amount
              },
              quantity: "1"
            }]
          }]
        });
      }}
      style={{
        label: 'buynow'
      }}
      options={{
        clientId,
        currency: currencyCode,
      }}
    />
  </Box>
}

export default atomize(QuarklyPaypalButton)({
  name: "QuarklyPaypalButton",
  effects: {
    hover: ":hover"
  },
  normalize: true,
  mixins: true,
  description: {
    en:
      "QuarklyPaypalButton — my awesome component",
  },
  propInfo: {
    amount: {
      title: "Amount",
      control: "input",
      category: "Item"
    },
    itemName: {
      title: "Name",
      control: "input",
      category: "Item"
    },
    itemDescription: {
      title: "Description",
      control: "text-area",
      category: "Item"
    },
    currencyCode: {
      title: "Currency code",
      control: "input",
      category: "Main",
    },
    clientId: {
      title: "Client ID",
      control: "input",
      category: "Main"
    }
  }
}, {
  amount: "1",
  currencyCode: "USD",
  clientId: "sb",
});
```

### 1.3 Страница с товаром

Создаем страницу с названием **Long Sleeve**. В настройках страницы указываем URL: **long-sleeve**.

![Page Settings](/scr/tutorials/integration-with-paypal-page-settings-url.png)

```jsx
<Link
	href="/index#"
	color="#000000"
	position="absolute"
	top="25px"
	left="25px"
	bottom="575.25px"
	height="36.75px"
	font="--headline3"
	text-decoration-line="initial"
	hover-color="--primary"
	transition="all --transitionDuration-normal ease 0s"
>
	&lt;
</Link>
<Section padding="80px 0 80px 0" sm-padding="60px 0 60px 0">
	<Override slot="SectionContent" flex-direction="row" md-flex-wrap="wrap" />
	<Box
		width="50%"
		display="flex"
		flex-direction="column"
		justify-content="space-between"
		md-width="100%"
		padding="0px 0px 0px 0px"
		lg-padding="0px 30px 0px 0px"
		md-padding="0px 0px 0px 0px"
		md-margin="0px 0px 30px 0px"
	>
		<Image max-width="340px"/src="https://images.unsplash.com/photo-1618354691229-88d47f285158?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=715&q=80" md-margin="0px 0px 20px 0px" align-self="center" />
	</Box>
	<Box
		width="50%"
		display="flex"
		flex-direction="column"
		justify-content="space-between"
		md-width="100%"
		align-self="center"
	>
		<Text margin="0px 0px 40px 0px" color="--dark" font="--headline1" md-margin="0px 0px 30px 0px">
			Long Sleeve
		</Text>
		<Text margin="0px 0px 40px 0px" color="--darkL2" font="--headline2">
			$25.00
		</Text>
		<Text margin="0px 0px 0px 0px" color="--darkL2" font="--base">
			<Strong
				overflow-wrap="normal"
				word-break="normal"
				white-space="normal"
				text-indent="0"
				text-overflow="clip"
				hyphens="manual"
			>
				Origin:
			</Strong>
			 Imported
			<br />
			<Strong
				overflow-wrap="normal"
				word-break="normal"
				white-space="normal"
				text-indent="0"
				text-overflow="clip"
				hyphens="manual"
			>
				Contents:
			</Strong>
			 100% Lightweight Cotton Jersey
			<br />
			<Strong
				overflow-wrap="normal"
				word-break="normal"
				white-space="normal"
				text-indent="0"
				text-overflow="clip"
				hyphens="manual"
			>
				Print Name:
			</Strong>
			 705
			<br />
			<Strong
				overflow-wrap="normal"
				word-break="normal"
				white-space="normal"
				text-indent="0"
				text-overflow="clip"
				hyphens="manual"
			>
				Care Instructions:
			</Strong>
			<br />
			Machine Wash Cold with like colors
			<br />
			Do not bleach
		</Text>
		<Components.QuarklyPayPal
			padding="20px 0px 20px 0px"
			amount="25"
			itemName="Long Sleeve"
			itemDescription="Long Sleeve Description"
			currencyCode="USD"
		/>
	</Box>
</Section>
```

Страница должна выглядеть так:

![Product Page](/scr/tutorials/integration-with-paypal-product-page.png)

Затем сделаем 2 копии страницы. Переименуем одну в **T-shirt Small Logo**, а другую в **T-shirt Big Logo**. Заменим ссылки на **t-shirt-small-logo** и **t-shirt-big-logo** соответственно.

Поменяем изображения, названия и описания для товаров (изображени для **T-shirt Small Logo и T-shirt Big Logo** можно взять с главной страницы)

Кроме этого, необходимо поменять пропсы у QuarklyPaypal компонента.

В категории **Item** нужно указать цену, название товара и его описание.

В категории **Main** нужно указать валюту и Client ID.

:::note
💡 Данные свойства должны быть одинаковы для всех товаров

:::

О том, как получить Client ID будет рассказано в следующем разделе.

## 2. Настройка PayPal аккаунта (Sandbox)

Cоздадим **Sandbox** (тестовую) версию приложения. Благодаря этой версии мы сможем проверить все методы оплаты без необходимости проводить реальную оплату.

Заходим на страницу [My Apps & Credentials](https://developer.paypal.com/developer/applications).

![My app and credentials](/scr/tutorials/integration-with-paypal-my-app-and-credentials.png)

Нажимаем **Create App**. Указываем название приложения и опять жмем Create App.

![Create new app](/scr/tutorials/integration-with-paypal-create-new-app.png)

![Sandbox app](/scr/tutorials/integration-with-paypal-my-quarkly-sandbox-app.png)

Копируем Client ID и в компоненты QuarklyPaypal каждого товара.

## 3. Проверяем оплату

Заходим на Sandbox Buisness Account. Получить данные для входа можно в разделе [Accounts](https://developer.paypal.com/developer/accounts).

Выбираем из списка аккаунт с типом **Business**, жмем **View/edit account**.

![Account list](/scr/tutorials/integration-with-paypal-account-list.png)

:::note
💡 Желательно это делать в отдельном браузере / режиме инкогнито, чтобы была возможность зайти с Personal Account для проверки работы оплаты со стороны покупателя.

:::

Переходим на [https://www.sandbox.paypal.com/us/signin](https://www.sandbox.paypal.com/us/signin) и вводим полученные **Email ID** и **System Generated Password**.

После авторизации мы попадаем на главную страницу, где у нас отображается сумма баланса в 5000$.

![Account dashboard](/scr/tutorials/integration-with-paypal-account-dashboard.png)

Таким же образом заходим с данными от аккаунта с типом **Personal**.

Интерфейс аккаунта с типом Personal будет отличаться:

![Dashboard Summary](/scr/tutorials/integration-with-paypal-account-dashboard-summary.png)

Проверим оплату:

![Checking Payment](/scr/tutorials/integration-with-paypal-checking-payment.png)

![Checking Alert](/scr/tutorials/integration-with-paypal-checking-alert.png)

После оплаты Buisness аккаунт будет выглядеть так:

![Dashboard after Payment](/scr/tutorials/integration-with-paypal-account-dashboard-after-payment.png)

![PayPal notification](/scr/tutorials/integration-with-paypal-notifications.png)

Посмотреть все заказы можно нажав **[View all items ready to ship](https://www.sandbox.paypal.com/listing/transactions?tab=activity&transactiontype=ITEMS_TO_SHIP)**

![All ready to ship items](/scr/tutorials/integration-with-paypal-all-items-ready-to-ship.png)

Со стороны Personal аккаунта эта страница будет выглядеть так:

![Personal account side](/scr/tutorials/integration-with-paypal-personal-account-side.png)

## 4. Настройка PayPal аккаунта (Live)

Для создания Live (production версии), необходимо перейти в [My Apps & Credentials](https://developer.paypal.com/developer/applications) и выбрать **Live.**

![PayPal live mode](/scr/tutorials/integration-with-paypal-live-mode.png)

![Live mode create app](/scr/tutorials/integration-with-paypal-live-mode-create-app.png)

![Live app API](/scr/tutorials/integration-with-paypal-live-app-api.png)

Копируем Client ID и в компоненты QuarklyPaypal каждого товара.

---