# Expense Tracker

A comprehensive expense and budget tracking application built with React, Vite, and Supabase.

## Features

### ✅ Expense Management (CRUD)
- **Create**: Add new expenses with amount, description, category, and date
- **Read**: View all expenses with filtering and search capabilities
- **Update**: Edit existing expenses with full form validation
- **Delete**: Remove expenses with confirmation dialog
- **Form**: Uses react-hook-form with Zod validation and ShadcnUI components

### 📊 Dashboard (Home Page)
- **Pie Chart**: Visualize expenses by category using Recharts
- **Bar Chart**: Daily expense tracking for the selected month
- **Summary Cards**: Total expenses, transaction count, average per transaction, active categories
- **Date Filtering**: Month picker to filter dashboard data
- **Real-time Updates**: Data automatically updates when expenses change

### 📁 Category Management
- **CRUD Interface**: Full category management with name and icon
- **User-scoped**: Categories are specific to each user
- **Icon Support**: Add emojis or text icons for visual identification
- **Usage Tracking**: See how many expenses use each category

### 🔍 Filtering & Search
- **Search**: Filter expenses by description or category name
- **Category Filter**: Filter by specific categories
- **Date Filters**: Today, This Week, This Month, or All Time
- **Real-time**: All filters update instantly as you type

## Tech Stack

- **Frontend**: React 18 with TypeScript
- **Build Tool**: Vite
- **Styling**: TailwindCSS + ShadcnUI
- **Charts**: Recharts
- **Database**: Supabase (PostgreSQL)
- **Authentication**: Supabase Auth
- **Forms**: react-hook-form + Zod
- **State Management**: @tanstack/react-query
- **Date Handling**: date-fns

## Getting Started

### Prerequisites

- Node.js 18+ 
- npm or yarn
- Supabase account

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd expense-tracker
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up Supabase**
   
   The project is already configured with:
   - **Supabase URL**: `https://rjqmjntcuhhcaenfmwoc.supabase.co`
   - **Supabase Anon Key**: Already included in the project

4. **Set up the database**
   
   Run the migration to create the required tables:
   ```bash
   # The migration file is already created at:
   # supabase/migrations/20241201000000_create_categories.sql
   
   # You can run this in your Supabase dashboard SQL editor
   ```

5. **Start the development server**
   ```bash
   npm run dev
   ```

6. **Open your browser**
   Navigate to `http://localhost:8080`

## Database Schema

### expenses table
```sql
CREATE TABLE expenses (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE,
  amount DECIMAL(10,2) NOT NULL,
  description TEXT,
  category_id UUID REFERENCES categories(id) ON DELETE SET NULL,
  date DATE NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

### categories table
```sql
CREATE TABLE categories (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE,
  name TEXT NOT NULL,
  icon TEXT,
  created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);
```

## Usage

### Authentication
- Users can sign up with email/password
- Authentication is handled by Supabase Auth
- All data is scoped to the authenticated user

### Adding Expenses
1. Navigate to the "Expenses" tab
2. Click "Add Expense"
3. Fill in the amount, description, category, and date
4. Submit the form

### Managing Categories
1. Navigate to the "Categories" tab
2. Click "Add Category" to create new categories
3. Edit or delete existing categories as needed

### Dashboard Analytics
- View the Dashboard to see expense analytics
- Use the month picker to view different time periods
- See breakdowns by category and daily spending patterns

### Filtering and Search
- Use the search bar to find specific expenses
- Filter by category using the dropdown
- Filter by date range (Today, Week, Month, All Time)

## Development

### Project Structure
```
src/
├── components/
│   ├── Dashboard.tsx          # Dashboard with charts
│   ├── ExpensesList.tsx       # Expense management with filtering
│   ├── CategoriesList.tsx     # Category management
│   ├── ExpenseForm.tsx        # Add/edit expense form
│   └── CategoryForm.tsx       # Add/edit category form
├── hooks/
│   ├── useAuth.tsx           # Authentication hook
│   ├── useExpenses.ts        # Expense data management
│   └── useCategories.ts      # Category data management
├── integrations/
│   └── supabase/
│       ├── client.ts         # Supabase client configuration
│       └── types.ts          # TypeScript types for database
└── pages/
    ├── Index.tsx             # Main application page
    ├── Auth.tsx              # Authentication page
    └── NotFound.tsx          # 404 page
```

### Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run lint` - Run ESLint

## Environment Variables

The following environment variables are already configured:

```bash
# Supabase Configuration (already set up)
VITE_SUPABASE_URL=https://rjqmjntcuhhcaenfmwoc.supabase.co
VITE_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InJqcW1qbnRjdWhoY2FlbmZtd29jIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTM5NTQ4OTMsImV4cCI6MjA2OTUzMDg5M30.tU4qD3_WFK-CqKwQ17DQfd5WEHOJcU1KSwhSlMCbLR4
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.