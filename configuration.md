# ⚙️ Конфигурация

## Файлы конфигурации

### `config.json`
Основная конфигурация ботов.

```json
{
  "bots": {
    "bot-1": {
      "name": "Moderation Bot",
      "prefix": "!",
      "intents": ["Guilds", "GuildMessages", "GuildMembers", "GuildBans"]
    },
    "bot-3": {
      "name": "Economy Bot",
      "prefix": "$",
      "intents": ["Guilds", "GuildMessages", "GuildMembers"]
    }
  }
}
```

### `.env`
Секретные переменные.

```env
# Токены ботов
BOT1_TOKEN=...
BOT2_TOKEN=...
BOT3_TOKEN=...
BOT4_TOKEN=...

# CryptoBot для донатов
CRYPTO_BOT_TOKEN=...
```

---

## Баланс экономики

Файл: `core/EconomyConfig.ts`

### Работа (`WorkConfig`)

```typescript
export const WorkConfig = {
    minEarn: 500,      // Минимальный заработок
    maxEarn: 2000,     // Максимальный заработок
    cooldown: 30 * 60 * 1000,  // 30 минут
    levelBonus: 5,     // +5% за каждый уровень
};
```

### Уровни (`LevelConfig`)

```typescript
export const LevelConfig = {
    xpMin: 15,         // Мин XP за сообщение
    xpMax: 40,         // Макс XP за сообщение
    xpCooldown: 30,    // Кулдаун XP (сек)
    baseXp: 100,       // Базовый XP для уровня
    xpMultiplier: 1.5, // Множитель роста
    levelReward: 1000, // Награда за уровень
};
```

### Майнинг (`MiningRates`)

Добавление новых видеокарт:

```typescript
export const MiningRates = {
    'gpu_новая': { rate: 5000, name: 'Новая карта', emoji: '💎' },
    // ...
};
```

### Бизнесы (`BusinessRates`)

Добавление новых бизнесов:

```typescript
export const BusinessRates = {
    'biz_новый': { income: 75000, name: 'Новый бизнес', emoji: '🏛️' },
    // ...
};
```

### Цены (`ShopPrices`)

После добавления предмета в Rates, добавьте цену:

```typescript
export const ShopPrices = {
    'gpu_новая': 2500000,
    'biz_новый': 10000000,
    // ...
};
```

### Чёрный рынок (`BlackmarketServices`)

```typescript
export const BlackmarketServices = [
    {
        id: 'remove_warn',
        name: 'Снятие предупреждения',
        description: 'Удаляет 1 варн',
        price: 50,
        emoji: '⚠️',
    },
    // ...
];
```

---

## После изменения конфигурации

1. **Пересоберите проект:**
   ```bash
   npm run build
   ```

2. **Обновите базу данных (для новых предметов):**
   ```bash
   node dist/scripts/seedItems.js
   ```

3. **Перезапустите ботов:**
   ```bash
   pm2 restart all
   ```

---

## Дизайн-система

Файл: `utils/components.ts`

### Иконки (`Icons`)

```typescript
export const Icons = {
    success: '✅',
    error: '❌',
    money: '💰',
    // ...
};
```

### Форматирование (`Format`)

```typescript
Format.bold('текст')      // **текст**
Format.mention('id')      // <@id>
Format.timestamp(date)    // <t:unix:R>
```

### Карточки

- `successCard(title, description, footer?)`
- `errorCard(title, description, footer?)`
- `infoCard(title, description, footer?)`
- `balanceCard(username, cash, bank, donate?)`
- `shopCard(items, page, totalPages)`
- `inventoryCard(username, items, total, page, totalPages, isOwner)`
- И многие другие...

