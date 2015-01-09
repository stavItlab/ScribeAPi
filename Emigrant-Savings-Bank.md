Emigrant Savings Bank Records: Mortgage and Bond Records
============================================

# Project Overview
## In a Nutshell
Extracting and structuring the building-level mortgage records from Emigrant Savings Bank, one of the first banks to cater to new immigrants in NYC, to create a dataset of financial information about the landholding and financial patterns of new NYC immigrants in the second half of the 19th century and augment our building-level understanding of places in NYC.

## Background
[Emigrant Savings Bank](https://en.wikipedia.org/wiki/Emigrant_Savings_Bank) is a bank located in NYC founded in 1850 by members of the Irish Emigrant Society and was set up predominantly to cater to the needs of new immigrants in New York, particularly Irish immigrants. While many of their records have been digitized and poured over by generations of genealogists, including through Ancestry.com, their real estate materials appear to be largely unknown and underutilized. 

These include their mortgage and bond records: loans taken out (we suspect mostly by relatively new immigrants) to buy properties and to mortgage existing real estate; an essential step in moving up in New York's economic strata.

We suspect building a keyword searchable, and structured index of names like this will have a tremendous appeal to genealogists for transcription, provide a new source of material for historians, and provide NYPL with useful location data for the NYC Space/†ime directory.

The collection belongs to Manuscripts and Archives, but the primary users are the Milstein Collection (coincidentally, the Milstein family owns Emigrant Savings Bank today).



As the finding aid describes these real estate materials:
> The Bond and Mortgage Books and Bond and Mortgage Ledgers record real estate transactions and have their own numbers which can be found in the Bond and Mortgage Name Index. The entries in the Bond and Mortgage Books include the date of approval, name of mortgagor, house number, size of the ground, description of the building, the amount of the loan, the name of the attorney, and in most cases a drawing of the location on a block map. There are also five Real Estate Loans Ledgers pertaining to the years 1902 to 1923. Information to be found in the Real Estate Loans Ledgers include the applicant’s name, the amount of money requested (at 5% interest) location of ground and building, material the building is to be made of, and the number of floors.

There are about 6,400 mortgages in the 10 reels that make up the Bond and Mortgage holdings, and another set relate to the ledgers.


## Data Fields
### In Existing Reel Metadata
* Reel/Book
* Capture Order
* General Year Range

### To Be Collected
* Bond & Mortgage Number
* Date Of Issue
* Mortgager (person)
* Location (geolocated)
 * Address Number (may be multiple)
 * Address Street (may be multiple)
 * In NYC? - BOOL - maybe we infer?
 * Borough (can probably default to Manhattan)
 * Cross Streets
* Ground Dimensions [ints + description]
* Description of Building [text, but might make sense to taxonomize]
* Value of land [sometimes these get confusing. Also can be appraised by the bank or by the owner]
* Value of Building

* Later valuation
 * Date
 * Reappraised value

* Amount
* Building Use Type
* Paid off (yes/no)

# Design Elements
[SAMPLE IMAGES](https://drive.google.com/a/nypl.org/folderview?id=0B7vD_dNzt2XrVjlhUmNOYmQwMDg&usp=sharing)
[tk]

## Transcription Elements
TK

### Anomalies
* Unreadable elements
* Almost all are located in Manhattan. However some aren't (Morsitania example)
* Some have images pasted over elements. Capture them? But also obscured elements (Morisitania example)
* Certain books have different templates. Do we want to anticipate that and know ahead of time? How do we specify these in the metadata? Should there be a way to do this kind of determination we provide for our users?


# Project Logistics
## Digitization
The entire collection has been microfilmed and has a [tremendously detailed finding aid](http://archives.nypl.org/uploads/collection/pdf_finding_aid/emigrant.pdf).

### Digitization Specification
In conversation with digitization vendors (see below), it appears the protocol for most microfilm digitizations is to _not_ output TIFFs. [//TODO FOR RIORDAN: Confirm this and also get quote for if we were to do TIFFs, just for giggles and for "easier" repository ingest].

> 10 reels
>
> 200 dpi [$40/reel] or 300 dpi [$60/reel] - still not 100% sure which we'll go with
>
> Delivery on a USB drive (to be shipped back with the reels)
> 
> Files to be organized into folders named by item call number and reel numbers (to be written on the outside of the boxes). Images to be named sequentially within those folders. [e.g.
> 
> Filetype: JPEG

### Vendors
We have identified [http://generationimaging.com/](Generation Imaging) as our microfilm digitizer of choice for this project.

> Here are the prices for tiffs if required by themselves or along side the JPEGs (200 dpi [$40/reel] or 300 dpi [$60/reel]).
> LZW compressed greyscale tiffs be $50 per roll for 200dpi and $70 per roll for the 300dpi.
> Uncompressed greyscale tiffs would be a $60 for 200dpI and $80 for the 300dpi. Would need a large external storage.

We're waiting on a final quote once we decide on the DPI and TIFF questions (decision relative to available budget).
