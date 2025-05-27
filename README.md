# Laravel Cookie Consent

**A lightweight, GDPR-compliant cookie consent system with minimal dependencies for Laravel 11**

[![Laravel Version](https://img.shields.io/badge/Laravel-11.x-red.svg)](https://laravel.com)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE.md)
[![Minimal Dependencies](https://img.shields.io/badge/Dependencies-Minimal-green.svg)](composer.json)

## ✨ Highlights

- **Zero external dependencies** - No Livewire, no Filament, no JS frameworks
- **Alpine.js & Vanilla JS** - Uses Alpine.js that comes with Laravel
- **GDPR-compliant** - Legally sound implementation with opt-in for all cookie types
- **Multilingual** - German, English, Spanish and Chinese included
- **Google Analytics Integration** - Dynamic loading and removal of GA scripts
- **Locale Cookie Management** - Stores language preferences only with consent
- **Blade Components** - Easy integration into existing Laravel applications
- **Tailwind CSS** - Elegant, customizable design (optional)
- **Mobile-First** - Fully responsive for all devices

## 🚀 Installation

```bash
composer require martin-schenk/laravel-cookie-consent
php artisan vendor:publish --provider="MartinSchenk\CookieConsent\CookieConsentServiceProvider"
```

## 🔧 Configuration

After publishing the package assets, you can configure the cookie consent system in `config/cookie-consent.php`:

```php
// config/cookie-consent.php
return [
    'google_analytics_id' => env('GOOGLE_ANALYTICS_ID', ''),
    
    'cookie_names' => [
        'consent' => 'cookieConsent',
        'locale' => 'locale',
    ],
    
    'cookie_lifetime' => 31536000, // 1 year in seconds
    
    'categories' => [
        'essential' => true,  // Always required
        'analytics' => false, // Optional
        'preferences' => false, // Optional
    ],
];
```

Add these settings to your `.env` file:

```env
# Cookie Consent Configuration
COOKIE_CONSENT_ENABLED=true

# Google Analytics ID
GOOGLE_ANALYTICS_ID=G-XXXXXXXXXX

# Cookie Settings (optional)
COOKIE_CONSENT_ANALYTICS=false
COOKIE_CONSENT_PREFERENCES=true
COOKIE_CONSENT_COOKIE_LIFETIME=31536000
```

## 📊 Usage

Include the cookie consent component in your main layout file:

```php
<!-- In your layout file -->
<x-cookie-consent::cookie-consent />
```

## 🔗 Adding a Cookie Settings Link to Your Footer

An important feature is the ability to reopen the cookie settings menu at any time. Here are different implementation options:

### Option 1: Direct JavaScript Call

```html
<a href="javascript:void(0);" onclick="window.openCookieSettings()" class="text-gray-400 hover:text-teal-400">
    Cookie Settings
</a>
```

### Option 2: For Complex Layouts (e.g., in a Vue or React component)

```javascript
// Trigger the cookie settings event
document.dispatchEvent(new CustomEvent('open-cookie-settings'));
```

### Option 3: Use as a Blade Component

```php
// In any of your Blade files:
<x-cookie-consent::settings-link class="text-gray-400 hover:text-teal-400" />
```

### Practical Example: Typical Footer Implementation

```php
<!-- Footer with legal links -->
<footer class="bg-gray-800 text-white py-6">
    <div class="container mx-auto">
        <div class="flex flex-wrap justify-center gap-4">
            <a href="{{ route('home') }}" class="text-gray-300 hover:text-white">Home</a>
            <a href="{{ route('imprint') }}" class="text-gray-300 hover:text-white">Imprint</a>
            <a href="{{ route('privacy') }}" class="text-gray-300 hover:text-white">Privacy Policy</a>
            
            <!-- Cookie Settings Link -->
            <a href="javascript:void(0);" 
               onclick="window.openCookieSettings()" 
               class="text-gray-300 hover:text-white">
                Cookie Settings
            </a>
        </div>
    </div>
</footer>
```

## 🌐 Supported Languages

This package comes with translations for:

- English (en)
- German (de)
- Spanish (es)
- Chinese (Simplified) (zh_CN)

You can publish the language files to customize them:

```bash
php artisan vendor:publish --provider="MartinSchenk\CookieConsent\CookieConsentServiceProvider" --tag="cookie-consent-lang"
```

## 🎨 Customizing Appearance

The cookie consent component uses Tailwind CSS by default. You can publish the views to customize the appearance:

```bash
php artisan vendor:publish --provider="MartinSchenk\CookieConsent\CookieConsentServiceProvider" --tag="cookie-consent-views"
```

## 🔒 How It Works

1. The package adds a cookie consent banner to your site
2. Users can accept all, reject all, or customize their preferences
3. Settings are saved in localStorage
4. Google Analytics is loaded dynamically only when user consents
5. Locale cookies are stored only with user consent
6. The settings can be reopened at any time via the footer link

## 📝 License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
