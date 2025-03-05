twilio
======

This package provides a library for interacting with
[Twilio's API](https://www.twilio.com/docs/api). Install using

```
$ cabal install twilio
```

Example
-------

You can create a REST API client and fetch the calls resources as follows

```hs
{-#LANGUAGE OverloadedStrings #-}

module Main where

import Control.Monad.IO.Class (liftIO)
import System.Environment (getEnv)
import Twilio
import Twilio.Calls as Calls
import Twilio.Messages

main :: IO ()
main = runTwilio' (getEnv "ACCOUNT_SID")
                  (getEnv "AUTH_TOKEN") $ do
  -- Print Calls.
  calls <- Calls.get
  liftIO $ print calls

  -- Send a Message.
  let body = PostMessage "+14158059869" "+14158059869" "Oh, hai" Nothing
  message <- post body
  liftIO $ print message
```

Testing
------------
Currently, our test suite makes calls to Twilio's API. This means that you will
be unable to test without a Twilio account.

To test on your local machine, set the environment variables `ACCOUNT_SID`,
`AUTH_TOKEN`, and `TEST_PHONE`. Twilio provides both test credentials and
non-test credentials. Make sure to use your **non-test credentials**.
Furthermore, the phone number must be able to make / receive calls, and be SMS
enabled.

The easiest way to provision a compatible phone number is to use the [Twilio
Website](https://www.twilio.com/console/phone-numbers/search) to buy a number,
with Voice / SMS / MMS capabilities.
