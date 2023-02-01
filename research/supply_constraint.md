# This is research piece on uluna supply constraint topic

The constrainedpool logic was part of the initial PR that formed TR back in June:
https://github.com/terra-money/classic-core/pull/778/files#diff-81594c0e59559d8705e1dd34fabbc9a8ab355da6b0d3b396686fecf1527567bb

It has been peer reviewed by Raider, Ed, Resolvence, Maxb to name a few. It has been tested with unit tests, integration tests, etc, etc.

The current target number of 2000000000000 was selected simply to avoid having to refactor all the other tests which would start bumping into issues. At the time it was my understanding that it was 2T. Being that sdk.Dec works differently then I initially assumed that number has to be corrected, but seeing how that was always the case, there was no real idea behind altering it until people could be convinced that  3568 covers the "supply constraint" or a new prop could be passed.
