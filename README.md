# Incident Response Table Top Exercise

An interactive web-based training platform for security teams to practice incident response procedures for phishing attacks and Azure cloud account compromise scenarios.

## Overview

This application provides a structured learning environment where security teams can:

- **Practice realistic scenarios** based on common attack patterns
- **Make incident response decisions** with immediate feedback on correctness
- **Learn best practices** through detailed explanations
- **Test knowledge** with a comprehensive quiz
- **Track progress** across multiple sessions

The application is designed to be deployed on GitHub Pages for easy team access without requiring a backend server.

## Features

### Scenarios

Five comprehensive scenarios covering:

1. **Suspicious Email Campaign Detected** (Beginner)
   - Recognize phishing attack indicators
   - Understand rapid incident response procedures
   - Learn the importance of evidence preservation

2. **Credential Compromise Confirmation** (Intermediate)
   - Respond to confirmed credential compromise
   - Protect privileged accounts
   - Perform forensic analysis of account activity

3. **Unusual Azure Portal Activity Detected** (Intermediate)
   - Identify Azure privilege escalation risks
   - Detect service principal misuse
   - Respond to cloud-based compromises

4. **Data Exfiltration Detected** (Advanced)
   - Investigate data exfiltration evidence
   - Assess impact scope
   - Coordinate compliance notifications

5. **Supply Chain Attack Vector** (Advanced)
   - Understand supply chain attack implications
   - Coordinate incident response across organizations
   - Share threat intelligence appropriately

### Quiz

Ten questions covering:
- Phishing attack response procedures
- Credential compromise handling
- Azure security threats
- Data exfiltration investigation
- Compliance and notification requirements

### Progress Tracking

- Automatic progress saving to browser localStorage
- Scenario completion tracking
- Quiz score history
- Overall exercise progress dashboard

## Getting Started

### For Users

1. Open the application URL (provided by your administrator)
2. Read each scenario carefully
3. Select your incident response decision
4. Review the explanation for the correct approach
5. Complete all scenarios
6. Take the final quiz to test your knowledge
7. Review your results and areas for improvement

### For Administrators/Deployers

See [DEPLOYMENT.md](./DEPLOYMENT.md) for detailed GitHub Pages deployment instructions.

## Technical Stack

- **Frontend Framework**: React 19 with TypeScript
- **Styling**: Tailwind CSS 4
- **UI Components**: shadcn/ui
- **Routing**: Wouter (client-side)
- **Build Tool**: Vite
- **Deployment**: GitHub Pages (static hosting)

## Project Structure

```
ir-tabletop-exercise/
├── client/
│   ├── public/
│   │   └── images/           # Visual assets (hero, icons)
│   ├── src/
│   │   ├── components/       # Reusable UI components
│   │   │   ├── ScenarioCard.tsx
│   │   │   ├── ScenarioDetail.tsx
│   │   │   └── Quiz.tsx
│   │   ├── hooks/            # Custom React hooks
│   │   │   └── useExerciseProgress.ts
│   │   ├── lib/              # Utility functions and data
│   │   │   └── exerciseData.ts
│   │   ├── pages/            # Page components
│   │   │   └── Home.tsx
│   │   ├── App.tsx           # Main app component
│   │   ├── main.tsx          # React entry point
│   │   └── index.css         # Global styles and theme
│   └── index.html            # HTML template
├── DEPLOYMENT.md             # GitHub Pages deployment guide
├── README.md                 # This file
└── package.json              # Dependencies and scripts
```

## Design Philosophy

The application follows **Security-Forward Minimalism** design principles:

- **Deep Navy + Cyber Red** color scheme reflecting professional security environments
- **Minimalist approach** reducing cognitive load during complex scenario navigation
- **Clear visual hierarchy** guiding users through incident response decisions
- **High contrast** and accessibility features ensuring all team members can participate
- **Timeline-based flow** naturally mirroring how incidents unfold in reality
- **Decisive interactions** reinforcing the weight of real incident response decisions

## Development

### Prerequisites

- Node.js 18+
- pnpm (or npm/yarn)

### Installation

```bash
# Install dependencies
pnpm install

# Start development server
pnpm dev

# Build for production
pnpm build

# Preview production build
pnpm preview
```

### Development Server

The development server runs on `http://localhost:3000` and includes:
- Hot module reloading
- TypeScript checking
- Automatic browser refresh

### Building for Production

```bash
pnpm build
```

This creates optimized static files in `dist/public/` ready for GitHub Pages deployment.

## Adding New Scenarios

To add new scenarios:

1. Edit `client/src/lib/exerciseData.ts`
2. Add a new scenario object to the `scenarios` array following this structure:

```typescript
{
  id: "unique-id",
  title: "Scenario Title",
  description: "Brief description",
  category: "phishing" | "account-compromise",
  difficulty: "beginner" | "intermediate" | "advanced",
  timeline: "HH:MM AM/PM - Day",
  context: "Detailed incident context...",
  decisions: [
    {
      id: "decision-id",
      text: "Decision text",
      consequence: "What happens if this decision is made",
      isCorrect: true/false,
      explanation: "Why this is correct/incorrect"
    }
  ],
  learningObjectives: ["Objective 1", "Objective 2"]
}
```

3. The scenario will automatically appear on the dashboard

## Adding Quiz Questions

To add quiz questions:

1. Edit `client/src/lib/exerciseData.ts`
2. Add a new question to the `quizQuestions` array:

```typescript
{
  id: "unique-id",
  question: "Question text?",
  options: ["Option 1", "Option 2", "Option 3", "Option 4"],
  correctAnswer: 0, // Index of correct option
  explanation: "Explanation of why this is correct",
  category: "phishing" | "account-compromise" | "mixed"
}
```

3. The question will automatically appear in the quiz

## Browser Support

- Chrome/Chromium (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Accessibility

The application includes:
- High contrast color scheme (WCAG AA compliant)
- Keyboard navigation support
- Screen reader friendly markup
- Clear focus indicators
- Semantic HTML structure

## Performance

- Lightweight static application (~600KB gzipped)
- No external API calls required
- Client-side progress storage (no server needed)
- Fast load times suitable for team training sessions

## Privacy & Security

- **No data collection**: User progress is stored only in browser localStorage
- **No backend server**: All data remains on the user's device
- **No authentication**: Open access for team members
- **No external dependencies**: Minimal third-party code

## Troubleshooting

### Progress not saving

**Issue**: Progress disappears after closing browser
**Solution**: Check that browser localStorage is enabled. Progress is stored locally and persists across sessions.

### Styles look broken

**Issue**: Colors or layout appears incorrect
**Solution**: 
1. Hard refresh browser (Ctrl+Shift+R)
2. Clear browser cache
3. Check that you're using a modern browser

### Scenarios not loading

**Issue**: Blank page or missing content
**Solution**:
1. Check browser console for errors (F12)
2. Verify JavaScript is enabled
3. Try a different browser

## Contributing

To contribute improvements:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is provided as-is for internal team training purposes.

## Support

For deployment questions, see [DEPLOYMENT.md](./DEPLOYMENT.md).

For technical issues or feature requests, create an issue in the GitHub repository.

## Learning Resources

### Incident Response Best Practices

- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [SANS Incident Response](https://www.sans.org/reading-room/whitepapers/)
- [Microsoft Azure Security Best Practices](https://docs.microsoft.com/en-us/azure/security/)

### Phishing Prevention

- [CISA Phishing Prevention](https://www.cisa.gov/phishing)
- [Microsoft Phishing Protection](https://docs.microsoft.com/en-us/microsoft-365/security/office-365-security/anti-phishing-protection)

### Azure Security

- [Azure Security Benchmark](https://docs.microsoft.com/en-us/security/benchmark/azure/)
- [Azure Sentinel Documentation](https://docs.microsoft.com/en-us/azure/sentinel/)

---

**Last Updated**: December 2025

**Version**: 1.0.0
