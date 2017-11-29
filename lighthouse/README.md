Based on [Quipper CircleCI Base Docker image](https://github.com/quipper/circleci-images/tree/master/base).

This image contains everything you need to run [Lighthouse](https://github.com/GoogleChrome/lighthouse):

- Latest stable Google Chrome
- NodeJS v6.11.1
- Yarn v1.3.2
- [Lighthouse](https://www.npmjs.com/package/lighthouse)

`CHROME_PATH` and `DISPLAY` environment variables are also set correctly as required by Lighthouse.
