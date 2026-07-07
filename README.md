# Portfolio Website - Static Hosting with S3 + CloudFront + CI/CD

A modern, responsive portfolio website hosted on AWS with automated CI/CD pipeline using CodePipeline.

## 🎯 Features

- ✅ **Responsive Design** - Mobile-friendly portfolio website
- ✅ **AWS S3 Hosting** - Secure and scalable static website hosting
- ✅ **CloudFront CDN** - Global content delivery with HTTPS
- ✅ **Automated CI/CD** - GitHub Actions workflow for continuous deployment
- ✅ **CodePipeline** - AWS CodePipeline for additional orchestration
- ✅ **Cache Optimization** - Intelligent caching strategies for performance
- ✅ **Error Pages** - Custom 404 error page

## 📁 Project Structure

```
portfolio-website/
├── index.html                 # Main portfolio page
├── css/
│   └── style.css             # Styling and responsive design
├── js/
│   └── main.js               # Interactive functionality
├── 404.html                  # Custom error page
├── .github/
│   └── workflows/
│       └── deploy.yml        # GitHub Actions workflow
├── cloudformation-template.yaml  # AWS infrastructure
└── README.md                 # This file
```

## 🚀 Quick Start

### Prerequisites

- Git installed on your laptop
- AWS Account (for deployment)
- GitHub Account
- AWS CLI configured locally (optional, for manual deployment)

### Step 1: Clone the Repository

```bash
git clone https://github.com/Farzana-sk/portfolio-website.git
cd portfolio-website
```

### Step 2: View Locally

Simply open `index.html` in your web browser to see the portfolio website:

```bash
# On macOS
open index.html

# On Windows
start index.html

# On Linux
xdg-open index.html
```

Or use a local server:

```bash
# Using Python 3
python -m http.server 8000

# Using Python 2
python -m SimpleHTTPServer 8000

# Using Node.js (if installed)
npx http-server
```

Then visit: `http://localhost:8000`

## 🏗️ AWS Deployment

### Option 1: Using GitHub Actions (Recommended - Easier)

1. **Setup AWS Credentials in GitHub**:
   - Go to your repository Settings → Secrets and variables → Actions
   - Add these secrets:
     - `AWS_ACCESS_KEY_ID` - Your AWS access key
     - `AWS_SECRET_ACCESS_KEY` - Your AWS secret key
     - `S3_BUCKET_NAME` - Your S3 bucket name
     - `CLOUDFRONT_DISTRIBUTION_ID` - Your CloudFront distribution ID

2. **Deploy**:
   ```bash
   git add .
   git commit -m "Deploy portfolio website"
   git push origin main
   ```
   The GitHub Actions workflow will automatically deploy your site!

### Option 2: Using CloudFormation

1. **Setup AWS Credentials**:
   ```bash
   aws configure
   ```

2. **Create CloudFormation Stack**:
   ```bash
   aws cloudformation create-stack \
     --stack-name portfolio-website \
     --template-body file://cloudformation-template.yaml \
     --parameters \
       ParameterKey=GitHubOwner,ParameterValue=Farzana-sk \
       ParameterKey=GitHubRepo,ParameterValue=portfolio-website \
       ParameterKey=GitHubToken,ParameterValue=your-github-token \
     --region us-east-1
   ```

3. **Monitor Stack Creation**:
   ```bash
   aws cloudformation describe-stacks \
     --stack-name portfolio-website \
     --region us-east-1
   ```

4. **Get Outputs** (Website URL, S3 Bucket, etc.):
   ```bash
   aws cloudformation describe-stacks \
     --stack-name portfolio-website \
     --query 'Stacks[0].Outputs' \
     --region us-east-1
   ```

## 🎨 Customization

### Edit Portfolio Content

1. **Home Section** - Edit `index.html` hero section
2. **About Section** - Update skills and bio
3. **Projects Section** - Add your own projects
4. **Styling** - Modify `css/style.css` for custom colors and fonts
5. **Interactivity** - Update `js/main.js` for custom behavior

### Color Scheme

Edit the CSS variables in `css/style.css`:

```css
:root {
    --primary-color: #667eea;
    --secondary-color: #764ba2;
    /* ... other variables ... */
}
```

## 💰 Cost Estimation

- **S3 Storage**: ~$0.023/GB (typically <$1/month)
- **CloudFront**: ~$0.085/GB (typical portfolio: $0.50-2/month)
- **Free Tier**: New AWS accounts get 12 months free tier
- **Total Monthly Cost**: $1-3 for typical portfolio traffic

## 🔒 Security Features

- ✅ S3 bucket is not publicly accessible
- ✅ CloudFront handles all public access
- ✅ HTTPS/TLS encryption enforced
- ✅ No sensitive data stored
- ✅ Version control enabled on S3

## 📊 Performance Optimization

- ✅ **CSS Caching**: 1 year for static assets
- ✅ **HTML Caching**: 5 minutes for dynamic content
- ✅ **CloudFront Edge Locations**: Global distribution
- ✅ **Gzip Compression**: Automatic with CloudFront
- ✅ **Lazy Loading**: Image lazy loading support

## 🔄 Deployment Workflow

```
1. Edit files locally
2. Commit to main branch
3. Push to GitHub
4. GitHub Actions triggers automatically
5. Website deploys to S3
6. CloudFront cache invalidated
7. Changes live in seconds
```

## 📝 Environment Variables

GitHub Actions secrets needed:

```
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key
S3_BUCKET_NAME=portfolio-website-123456789
CLOUDFRONT_DISTRIBUTION_ID=E1234ABCD
```

## 🐛 Troubleshooting

### Site not updating after push
- Clear CloudFront cache (done automatically in workflow)
- Clear browser cache (Ctrl+Shift+Delete)
- Check GitHub Actions logs for errors

### 404 errors on deployment
- Ensure `.github/workflows/deploy.yml` is in repo
- Check AWS credentials in GitHub Secrets
- Verify S3 bucket and CloudFront distribution IDs

### AWS Credentials not working
```bash
# Test AWS credentials
aws sts get-caller-identity

# If fails, reconfigure:
aws configure
```

## 📚 Resources

- [AWS S3 Documentation](https://docs.aws.amazon.com/s3/)
- [CloudFront Documentation](https://docs.aws.amazon.com/cloudfront/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [AWS CLI Reference](https://docs.aws.amazon.com/cli/latest/userguide/)

## 📞 Support

For issues or questions:
1. Check the [Troubleshooting](#-troubleshooting) section
2. Review GitHub Issues in the repository
3. Check AWS CloudFormation Events for deployment errors

## 📄 License

This project is open source and available under the MIT License.

---

**Happy Portfolio Hosting! 🚀**

Made with ❤️ by Farzana
