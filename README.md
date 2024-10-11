# NextJS Toolbox

## Eslint

Mettre à jour eslint vers `eslint v9` :

```bash
pnpm up -i -latest
```

- [Config `eslint v8`](./eslint/.eslintrc.json)
- [Config `eslint v9`](./eslint/eslint.config.mjs)

Installer les dépendances :

```bash
pnpm i -D @eslint/compat @eslint/js eslint-plugin-react-hooks eslint-plugin-react eslint-plugin-tailwindcss globals typescript-eslint @next/eslint-plugin-next
```

## Types

Typages pour les différents pages avec Nextjs : copier [`@/types/next.ts`](./types/next.ts)

## Environnement

Typage des variables d'environnent avec `@t3-oss/env-nextjs`.

Installation :

```bash
pnpm i @t3-oss/env-core zod
```

Config : copier [`@/lib/env.ts`](./lib/env.ts)

## TailwindCSS

### Utilisation du dossier src

Utilisation de l'alias dans `tsconfig.json` :

```json
{
  "compilerOptions": {
    // ...
    "paths": {
      "@/*": [
        "./src/*"
      ]
    }
  },
}
```

Ajouter le dossier `src/` dans `tailwind.config.ts`

```js
module.exports = {
  content: ["./src/**/*.{js,ts,jsx,tsx,mdx}", "./app/**/*.{js,ts,jsx,tsx,mdx}"],
  theme: {
    // ...
  },
}
```

### Typography

Installer le module typography :

```bash
pnpm i -D @tailwindcss/typography
```

Mettre à jour `tailwind.config.ts` :

```js
module.exports = {
  theme: {
    // ...
  },
  plugins: [
    require('@tailwindcss/typography'),
    // ...
  ],
}
```

### Composants tailwindcss

Installation :

```bash
pnpm i react-twc
```

Configuration :
Copier [`@/lib/twx.ts`](./lib/twx.ts)

## Prisma

Installation :

```bash
pnpm i @prisma/client @auth/prisma-adapter
pnpm i -D prisma
```

Initialisation de prisma :

```bash
pnpx prisma init
```

Modification des variables d'environnement :

```yml
DATABASE_URL=postgresql://USER:PASSWORD@HOST:PORT/DATABASE?schema=SCHEMA
```

Configuration : Copier [`@/lib/db.ts`](./lib/db.ts)

Migrer les données :

```bash
pnpx prisma migrate dev
```

### Ajout de seeding

Ajout d'un fichier `seed.ts` dans le dossier `/prisma`.

Modifier `package.json` :

```json
{
  "scripts": {
    // ...
  },
  "prisma": {
    "seed": "ts-node --compiler-options {\"module\":\"CommonJS\"} prisma/seed.ts"
  },
  // ...
}
```

Il est maintenant possible de seeder avec :

```bash
pnpx prisma db seed
```

## Safe Actions

## ShadCN

### Formulaire

Utilisation simplifiée de formulaire avec [`@/components/form.tsx`](./components/form.tsx).

Voici un exemple de formulaire :

```tsx
export const FormComponent = () => {
  const form = useZodForm({
    schema, //schema
    defaultValues, // defaultValues
  });

  const handleSubmit = async () => {};

  return (
    <Form form={form} onSubmit={handleSubmit}>
      <FormField
        name=""
        control={form.control}
        render={({ field }) => (
          <FormItem>
            <FormLabel></FormLabel>
            <FormControl>
              <Input {...field} />
            </FormControl>
            <FormMessage />
          </FormItem>
        )}
      />
      <Button type="submit"></Button>
    </Form>
  );
};
```
