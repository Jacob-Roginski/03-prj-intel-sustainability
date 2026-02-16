# Testing Guide - Intel Sustainability Website

This guide helps verify that all rubric requirements are met.

## Rubric Checklist

### 1. RTL Adaptation (15 pts)
**What to test:** Verify the website correctly applies RTL layout when switching to Arabic.

**How to test:**
1. Open the website in your browser
2. Click the **AR** button in the top navbar
3. Observe the following changes:
   - Text alignment should change from left to right
   - The `lang` attribute should change from `en` to `ar` (inspect with DevTools)
   - The `dir` attribute should change from `ltr` to `rtl`
   - Timeline cards should reverse their order
   - All text should right-align
   - Arrow icons in the accordion should rotate

**Expected behavior:**
- Smooth 0.3s transition when switching
- All page elements respect RTL direction
- Navbar brand and buttons repositioned for RTL
- Margin and padding values correctly flipped

**To test in Console:**
```javascript
setLanguage('ar')  // Switch to Arabic/RTL
setLanguage('en')  // Switch back to English/LTR
```

---

### 2. Responsive Three-Column Section (10 pts)
**What to test:** The features section uses Bootstrap grid and includes icons and buttons.

**How to test:**
1. On desktop (1024px+): Three columns side-by-side
2. On tablet (768px-1023px): Two columns on first row, one on second
3. On mobile (<768px): Single column layout
4. Verify each column has:
   - ✓ Icon (Lightning, Shield, Thumbs Up)
   - ✓ "Learn More" button
   - ✓ Consistent styling and spacing

**Preview at different sizes:**
- Press F12 to open DevTools
- Click the device icon (responsive design mode)
- Test at: 375px (mobile), 768px (tablet), 1024px (desktop)

---

### 3. Subscription Form & Footer (10 pts)
**What to test:** A styled subscription form and footer are present and properly designed.

**How to test:**
1. Scroll to the "Stay Updated on Sustainability" section
2. Verify the form includes:
   - ✓ Email input field with placeholder
   - ✓ Full Name input field
   - ✓ Subscribe button
   - ✓ Proper labels and helper text
   - ✓ Visual feedback on focus

3. Scroll to footer
4. Verify the footer includes:
   - ✓ About section
   - ✓ Quick Links
   - ✓ Social media icons
   - ✓ Certifications
   - ✓ Copyright notice
   - ✓ Proper styling and colors

**Test form submission:**
- Enter an email and click Subscribe
- An alert should confirm subscription
- Form should reset

---

### 4. Accessibility Improvements (15 pts)
**What to test:** The site meets WCAG accessibility standards (Lighthouse score 90+).

**How to test with Lighthouse:**
1. Open DevTools (F12)
2. Click "Lighthouse" tab
3. Click "Analyze page load"
4. Check the Accessibility score (target: 90+)

**Manual accessibility checks:**
1. **Color Contrast:**
   - Text should be readable against background
   - Intel Blue (#0071C5) on white has good contrast
   - White text on blue background has good contrast

2. **Alt Attributes:**
   - Right-click images → "Inspect"
   - All `<img>` tags should have `alt` attributes
   - Examples:
     - `alt="Intel Logo"`
     - `alt="Intel founding"`
     - `alt="RISE strategy launch"`

3. **Form Labels:**
   - Email input has `<label for="email-input">`
   - Name input has `<label for="name-input">`
   - Required fields marked with red asterisk

4. **ARIA Attributes:**
   - Language buttons have `aria-label`
   - Form fields have `aria-required`, `aria-describedby`
   - Accordion has `aria-expanded`, `aria-controls`

5. **Keyboard Navigation:**
   - Press **Tab** to navigate
   - You should be able to reach all buttons and form inputs
   - Visible focus indicator on buttons

---

### 5. LevelUp: Auto-Detect Language & Adjust Layout (10 pts bonus)
**What to test:** JavaScript automatically adjusts layout based on browser language.

**How to test:**
1. Open DevTools (F12) → Console
2. Test language detection:
   ```javascript
   // Check current language
   document.documentElement.lang  // Should show 'en' or 'ar'
   document.documentElement.dir   // Should show 'ltr' or 'rtl'

   // Manually switch
   setLanguage('ar')
   setLanguage('en')

   // Check localStorage
   localStorage.getItem('preferredLanguage')  // Shows saved preference
   ```

3. **Auto-detection:**
   - The website remembers your language choice in localStorage
   - If you refresh, the page stays in your selected language
   - Clear cache and refresh - it will try to detect your browser language

**Change browser language to test auto-detection:**
- Chrome: Settings → Languages → Change language
- Firefox: about:preferences → Language
- Clear browser cache to reset
- Reload page to see auto-detection

---

### 6. LevelUp: Enhance Interactivity (10 pts bonus)
**What to test:** An interactive Bootstrap component enhances functionality.

**What was implemented:** Accordion FAQ section

**How to test:**
1. Scroll to "Sustainability FAQs" section
2. Click any question button
3. Verify:
   - ✓ The answer expands smoothly
   - ✓ Only one answer visible at a time
   - ✓ Button background changes to Intel Blue (#0071C5)
   - ✓ Chevron icon rotates
   - ✓ Works on all devices (responsive)

4. **Test in RTL mode:**
   - Click AR button
   - The accordion should still work
   - Chevron should rotate in RTL direction
   - Text should right-align

5. **Accessibility:**
   - Tab to focus buttons
   - Press Enter/Space to open/close
   - `aria-expanded` attribute shows current state

---

## Quick Verification Checklist

- [ ] Navbar has EN and AR buttons
- [ ] Clicking AR switches text direction to right-to-left
- [ ] Features section shows 3 columns on desktop, responsive on mobile
- [ ] Each feature has icon, title, description, and "Learn More" button
- [ ] Subscription form is styled and functional
- [ ] Footer is present with multiple columns
- [ ] Accordion FAQ section is clickable and expands/collapses
- [ ] All images have alt text
- [ ] Form labels are properly associated
- [ ] Lighthouse accessibility score is 90+
- [ ] Keyboard navigation works (Tab through all interactive elements)
- [ ] RTL layout works in Arabic mode
- [ ] Accordion works in both LTR and RTL modes

---

## Browser DevTools Tips

**Inspect Element (Right-click → Inspect):**
```html
<!-- Check for aria attributes -->
<button aria-label="Switch to Arabic" aria-expanded="false">AR</button>

<!-- Check for alt text -->
<img src="path.jpg" alt="Descriptive text" />

<!-- Check dir attribute -->
<html lang="ar" dir="rtl">

<!-- Check data attributes -->
<button data-bs-toggle="collapse" aria-controls="collapseOne">
```

**Console Tests:**
```javascript
// Check current direction
document.documentElement.dir

// Check language
document.documentElement.lang

// Toggle language
setLanguage('ar')
setLanguage('en')

// Check form validation
document.getElementById('email-input').required

// Check localStorage
localStorage.getItem('preferredLanguage')
```

---

## Score Calculation

| Category | Points | Status |
|----------|--------|--------|
| RTL Adaptation | 15 | Test switching languages |
| 3-Column Responsive | 10 | Check at different breakpoints |
| Form & Footer | 10 | Verify presence and styling |
| Accessibility | 15 | Run Lighthouse audit |
| **Subtotal** | **50** | |
| LevelUp: Language Detection | 10 | Check auto-detect & localStorage |
| LevelUp: Interactivity (Accordion) | 10 | Click FAQ section |
| **Total Possible** | **70** | |

---

## Common Issues & Solutions

**Issue:** Lighs House score below 90
- **Solution:** Check for missing alt attributes, improve contrast, ensure form labels are linked

**Issue:** RTL not switching
- **Solution:** Make sure JavaScript is enabled, check browser console for errors

**Issue:** Accordion not opening
- **Solution:** Ensure Bootstrap JS is loaded (check DevTools Network tab), check browser console

**Issue:** Timeline not scrolling in RTL
- **Solution:** Timeline should reverse naturally with `direction: rtl` CSS

---

For questions, refer to the copilot-instructions.md file or console logs (F12 → Console).
