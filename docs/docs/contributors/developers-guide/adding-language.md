# How to add a language

1. A language must be added into [Crowdin](https://crowdin.com/project/mealie). This is typically done by hay-kot, and should be asked directly onto the [Discord server](https://discord.gg/QuStdQGSGK) in the #translation channel.
2. After the language is added, an automatic PR is created and accepted. This can take some hours.
3. Some files needs to be adapted, check the Changes required section here under

## Changes required

Another commit is required so that the language is taken into account.
You can find an example commit [here](https://github.com/mealie-recipes/mealie/pull/4004/commits/0e65dd72d9ea6e35ab7caaf8513393cee7e0e9e9)

**gen_ts_locales.py (dev/code-generation/gen_ts_locales.py)**

A line has to be added with this format :

```
    "[Locale]": LocaleData(name="[Localized name] ([English name])"),
```

where :

- **Locale** is the ICU locale with the language followed by an underscore and the country in uppercase : fr-FR, en-US, es-ES
- **Localized name** is the name of the language in the language itself : Français, English, Español
- **English name** is the name of the language translated into english : French, Spanish, ..

**available-locales.ts (frontend/composables/use-locales/available-locales.ts)**

Add a block specifying the language available for the frontend :

```
    {
        name: "[Localized name] ([English name])",
        value: "[Locale]",
        progress: 100,
        dir: "ltr",
    },
```

**Date time format (frontend/lang/dateTimeFormats/[locale].json)**

A file needs to be added for the date time formats
Follow the structure of other languages available

**nuxt.config.js (frontend/nuxt.config.js)**

Two lines needs to be added here, one in the i18n locales
```
    { code: "[locale]", file: "[locale].json" },
```
and one in the i18n dateTimeFormats :
```
    "[locale]": require("./lang/dateTimeFormats/[locale].json"),
```

**vuetify.options.js (frontend/vuetify.options.js)**

Add a lang locale

```
    "[locale]": locale.[language],
```

**validators.py (mealie/schema/_mealie/validators.py)**

Add a language for the schema validators

```
    "[locale]",
```
