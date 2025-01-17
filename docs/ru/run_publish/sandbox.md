# The Sandbox

В нашем предполагаемом сценарии использования нода SubQuery обычно запускается доверенным хостом, и код проекта SubQuery, отправленный пользователем ноде, не является полностью надежным.

Некоторый вредоносный код может атаковать хост или даже скомпрометировать его, а также нанести ущерб данным других проектов на том же хосте. Поэтому мы используем защищенный механизм Sandbox [VM2](https://www.npmjs.com/package/vm2) для снижения рисков. Это позволяет:

- Безопасно запускать ненадежный код в изолированной среде, и вредоносный код не получит доступа к сети и файловой системе хоста, кроме как через открытый интерфейс, который мы внедрили в изолированную среду.

- Безопасно вызывать методы и обмениваться данными и обратными вызовами между изолированными средами.

- Обладать иммунитетом ко многим известным методам атаки.


## Ограничения

- Ограниченный доступ к определенным встроенным модулям, только`assert`, `buffer`, `crypto`,`util` и `path` занесены в белый список.

- Мы поддерживаем [сторонние модули](../create/mapping/polkadot.md#third-party-libraries) написанные на **CommonJS** и **hybrid** библиотеки, такие как `@polkadot/*`, которые используют ESM по умолчанию.

- Любые модули, использующие `HTTP` и `WebSocket`, запрещены.
