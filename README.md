# GWRFC donation receipt maker

## Start on your Mac

1. Unzip this package.
2. Copy index.html to TRC_TB1/02-GWRFC/00-financials/donation-receipt-maker/, replacing the empty file.
3. Double-click index.html to open it in your browser. No installation is needed. Downloads work offline; emailing requires internet access.
4. Paste spreadsheet columns in this order: Name, Amount, Donation date. An optional fourth column supplies Donation type; an optional fifth supplies Email address. Headers are optional. Comma-separated CSV with quoted fields is also supported.
5. Use YYYY-MM-DD dates, or select the appropriate US/UK slash-date format. Amounts are USD.
6. Open Receipt wording & board signature and review the names and wording before issuing receipts. An optional receipt statement can be added there.
7. Click Review donations. Select any donor to inspect their receipt, then download an individual PDF or all receipts as a ZIP.

Each row is a separate donation. Duplicate names are kept and filenames include the row number to avoid collisions. Invalid input blocks the whole batch. Maximum batch: 500 donations. Downloaded PDFs are high-resolution image PDFs; text is not selectable. Close or reload the page to discard input and reset settings. Settings edits last only for the open page; change the defaults in index.html to make them permanent.

The crest is embedded in index.html. There are no external scripts, analytics, or stored donor records. Emailing sends the recipient, message, and PDF through Cloudflare and Resend. Do not upload donor spreadsheets or generated receipts to the website repository. The website itself has no login.

## Publish with GitHub Pages

1. Create a GitHub repository, for example donation-receipt-maker. A public repository works with GitHub Free.
2. Upload index.html to the repository root. You may also upload this README. No build process or dependencies are needed.
3. In repository Settings > Pages, choose Deploy from a branch, main, / (root), and Save.
4. Wait for GitHub to publish, then use Visit site from the Pages settings.

## Use your existing domain

Recommended address: donationreceipts.gwmensrugby.com. This gives the tool its own subdomain.

1. In that repository's Settings > Pages > Custom domain, enter donationreceipts.gwmensrugby.com and Save BEFORE adding the DNS record.
2. In the DNS settings for gwmensrugby.com, create a CNAME record:

   | Type | Name / Host | Target / Value |
   | --- | --- | --- |
   | CNAME | donationreceipts | YOUR-GITHUB-USERNAME.github.io |

   Replace YOUR-GITHUB-USERNAME with the account or organization that owns the repository. The target contains no https:// prefix and no repository path.
3. Wait for the DNS check and HTTPS certificate to become available, then select Enforce HTTPS in GitHub Pages settings. DNS/certificate updates may take up to 24 hours.
4. Keep the CNAME file GitHub adds to your repository when updating the site.

If you want to use gwmensrugby.com itself rather than a subdomain, that requires apex-domain DNS configuration and will change where the main domain points. Use GitHub's apex-domain instructions below once you have chosen that option.

The email Worker is deployed separately. These local website changes still need publishing to GitHub Pages.

## Official setup references

- https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
- https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

## Email receipts

The website connects to https://gwrfc-receipts-email.gwrfcaa.workers.dev/. Review donations, enter the sending password, and select an individual receipt, all receipts, or a test to your own address. Confirm the recipients before sending. Rows without email addresses are skipped. Each message includes the receipt wording without the table and an attached PDF.

Cloudflare secrets: RESEND_API_KEY and SEND_PASSWORD (at least 24 characters). Never put these values in the HTML or repository. For a GitHub Pages address outside the configured domains, add its exact origin to ALLOWED_ORIGINS in Cloudflare.

Sending results mean accepted by the email service, not confirmed delivery. The open page skips already accepted identical messages and reuses request IDs for unchanged retries. Reloading clears this protection; check Resend before retrying after a reload or uncertain result. Batch sending stops on the first error.
