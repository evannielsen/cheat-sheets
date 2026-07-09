# Serving the Cheat Sheets Locally

This project is built with Jekyll and can be served locally for development and testing.

## Prerequisites

Make sure you have Ruby installed on your system. If not, install it from [https://www.ruby-lang.org/](https://www.ruby-lang.org/).

## Setup Instructions

1. **Install required gems**:
   ```bash
   bundle install
   ```

2. **Serve the site locally**:
   ```bash
   bundle exec jekyll serve
   ```

3. **Access the site**:
   Open your browser and navigate to [http://127.0.0.1:4000](http://127.0.0.1:4000)

## Development Notes

- The site will automatically rebuild when you make changes
- Use `Ctrl+C` to stop the development server
- All content is authored in Markdown with CSS classes applied via inline HTML
- The site uses a shared layout (`_layouts/default.html`) and centralized CSS

## Troubleshooting

If you encounter any issues:

1. Make sure all gems are properly installed by running `bundle install`
2. For Windows users, if you get polling warnings, add the following to your Gemfile:
   ```ruby
   gem 'wdm', '>= 0.1.0'
   ```
   Then run `bundle install` again.