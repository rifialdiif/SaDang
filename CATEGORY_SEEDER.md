# Category Seeder

This project includes an automatic category seeder that populates default expense categories for new users.

## Features

### Automatic Seeding
- **On Signup**: New users automatically receive 16 default expense categories
- **No Manual Action Required**: Categories are seeded in the background during registration

### Manual Seeding
- **Seed Button**: Available in the Categories page for existing users
- **Smart Detection**: Only adds categories that don't already exist
- **Non-destructive**: Won't overwrite existing categories

## Default Categories

The following categories are automatically added:

| Category | Icon |
|----------|------|
| Food & Dining | 🍔 |
| Transportation | 🚗 |
| Shopping | 🛍️ |
| Entertainment | 🎬 |
| Bills & Utilities | 💡 |
| Healthcare | 💊 |
| Education | 📚 |
| Travel | ✈️ |
| Groceries | 🛒 |
| Housing | 🏠 |
| Insurance | 🛡️ |
| Personal Care | 💅 |
| Subscriptions | 📱 |
| Gifts & Donations | 🎁 |
| Business | 💼 |
| Other | 📊 |

## Usage

### For New Users
1. Sign up for a new account
2. Default categories are automatically added after successful registration
3. Visit the Categories page to see your pre-populated categories

### For Existing Users
1. Go to the Categories page
2. Click the "Seed Categories" button
3. Any missing default categories will be added

### Manual Seeding via Script

You can also run the seeder manually for a specific user:

```bash
# Install dependencies first
npm install

# Run the seeder script with a user ID
node seed-categories.js <user_id>
```

## Technical Details

### Files
- `src/lib/categorySeeder.ts`: Main seeder class with seeding logic
- `seed-categories.js`: Standalone script for manual seeding
- `src/pages/Auth.tsx`: Modified to seed categories on signup
- `src/components/CategoriesList.tsx`: Added manual seed button

### Database Schema
Categories are stored in the `categories` table with the following structure:
- `id`: UUID (auto-generated)
- `name`: String (category name)
- `icon`: String (emoji or icon)
- `user_id`: UUID (foreign key to users)
- `created_at`: Timestamp

## Customization

To modify the default categories:
1. Edit the `DEFAULT_CATEGORIES` array in `src/lib/categorySeeder.ts`
2. Update the same array in `seed-categories.js` if using the standalone script
3. The changes will apply to new users and manual seeding operations