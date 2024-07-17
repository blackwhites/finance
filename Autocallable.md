# Autocallable

An autocallable is a structured product which offers an opportunity for both early redemption at a predefined cash amount and high coupons. Both these opportunities are linked to the performance of the underlying which can be either of the following:

- The spot of a single asset.
- The worst performance in a defined basket of assets.
  - This is simply the lowest value of all the assets in the basket, where the value of each asset is calculated as the spot of the asset at that time / the initial spot of that asset.

There are regular observation dates (or coupon dates), usually once a year. On each of these dates, whether the instrument is early redeemed and/or whether the high coupon is paid depends on the performance of the underlying relative to two predefined barriers, the Coupon Barrier and the Autocall Barrier. That is:

- If the underlying is at or above the coupon barrier, the coupon is paid.
- In addition, if the underlying is at or above the autocall barrier, the product redeems automatically and the investor (or holder) receives the predefined cash amount, or notional, from the issuer of the product.
  - When the notional is paid, either immediately or at the next coupon payment date, depends on the instrument definition.
  - Because the autocall barrier is generally set above the coupon barrier, in this case the investor may also receive the coupon payment, therefore not only getting the investment back but also benefitting from an elevated return after, for example, only one year.
  - Whether or not the investor also receives the coupon payment depends on the instrument definition.

If there is no early redemption, the product continues to the next observation date, where there is again the possibility of early redemption.

Even if the coupon barrier is not breached, as long as the investor entered into a Memory variation of the autocallable, then the opportunity of receiving a high coupon for that coupon date is not lost. This is because in the memory variation the available coupon increases on each observation date that the coupon barrier is not triggered.

In addition, if the instrument includes a guaranteed coupon, on each coupon payment date that the instrument is still alive the investor also receives the defined guaranteed coupon.

As a structured product the autocallable can be wrapped as any of the following:

1. **Bond**
   - If you choose the Bond wrapper, the bond issuer pays the bond holder interest (the coupon) on predefined dates (the coupon dates) and also repays the principal (either on the bond's maturity or at an earlier time is the instrument is redeemed early). An advantage is that in addition to the coupon payments, the payout of the optional option(s) at expiry cannot be negative (unlike the option version of this instrument).
   - It is important here to note that whatever happens, the principal is always repaid, although if on the expiry date the investor is exposed to the downside/upside of the underlying the investor will still have to make a payout.

2. **Option**
   - If you choose the Option wrapper, then the autocallable issuer pays the autocallable holder interest (the coupon) on predefined dates (the coupon dates). In addition, there is a payout of the optional option(s) at expiry. Unlike the bond version, there is no notional repayment which necessarily makes the instrument much cheaper. However, there is the added risk that the payout of the optional option(s) at expiry may be negative.

3. **Swap**
   - If you choose the Swap wrapper, the autocallable is combined with a swap's floating leg. This means that the autocallable issuer pays the autocallable holder interest (the coupon) on predefined dates (the coupon dates), while the autocallable holder pays a series of cash flows to the autocallable issuer on predefined payment dates. This lets you create a structure whereby the holder does not have to pay a premium up front. Rather the holder can choose to pay for the instrument in the form of predefined cash flows. In addition, there is a payout of the optional option(s) at expiry.
   - Unlike the bond version, there is no notional repayment which necessarily makes the instrument much cheaper. However, there is the added risk that the payout of the optional option(s) at expiry may be negative.

In addition, you can optionally include up to three "Options at Expiry".

A quanto version of the autocallable is also supported.

## Instrument Characteristics

In addition to the guaranteed coupon, the instrument's payout is dependent on the instrument's characteristics, as defined here:

### Autocall Barrier

The autocall barrier is defined as a certain percentage of the underlying's initial spot (i.e., its spot at the time the instrument was defined). So, for example, if the autocall barrier is set to 130% and the initial spot of the underlying was 2247, the trigger is 130% of 2247, i.e., 2921.1.

On each relevant date (this is the coupon observation date if the barrier is set to European or any date if the barrier is set to be continuously monitored) the underlying is monitored and then compared to the autocall barrier. If on that date the underlying trades at or above the autocall barrier, the product is then automatically redeemed at a predefined cash amount. That is, the investor receives the principal back.

The resultant payout when the autocall barrier is breached is therefore calculated as follows:

```
100% + coupon (tc)
```

When the actual principal is repaid depends on the instrument definition—i.e., whether you defined the payment to be made immediately on the autocall barrier being hit or only on the next coupon payment date after the autocall barrier is hit.

- If you choose to receive the payment immediately, the actual payment date takes the defined settlement delay into account. So, for example, if the settlement delay is set to 2 days and the autocall barrier is hit on 6 February, the actual payment will be made on 8 February. The settlement delay is defined in the Coupon Dates & Rates window, which is accessed by clicking the Coupon Dates & Rates button.
- If the coupon(s) and/or guaranteed coupon are to be paid as well as the principal, these are always paid together with the principal, either immediately after the barrier is hit or on the next coupon payment date. All future payments are cancelled.

When calculating an autocallable, the system also calculates the probability that the autocallable instrument will be knocked out, i.e., that the autocall barrier will be hit, on a relevant date. This result is displayed in the Single Option page as the Autocall Probability result and in the Portfolio page as the Hit Probability result.

### Coupon Barrier

The coupon barrier is the spot level above which a coupon will be paid. It is defined as a percentage of the underlying's initial spot (i.e., its spot at the time the instrument was defined). For example, if the coupon barrier is set to 110% and the initial spot of the underlying was 2000, it is 2200.

The actual payment depends on both of the following:

- The Coupon Style selected and, if you selected binary, if you also selected a Memory variation of the instrument.
- On whether the Autocall Barrier is set to be continuously monitored or not and on whether it is hit.

If it is a binary style, on each relevant date (i.e., the coupon observation date if the barrier is set to European or any date if the barrier is set to be continuously monitored) that the product is still alive (i.e., the defined Autocall Barrier has not been breached), the underlying is monitored. The coupon is only paid if the underlying on that date is above the Coupon Barrier.

If it is an accrual style, on each observation (or accrual frequency) date that the product is still alive, the underlying is monitored. The coupon is only accrued for that date if the underlying on that date is above the Coupon Barrier. The coupon paid on the next coupon date necessarily depends on the coupon accrued over the coupon period itself.

If the coupon style is set to:

- Binary and the autocall barrier is set to be continuously monitored:
  - If the autocall barrier is hit and if the coupon barrier is also set to continuous monitoring and it is hit on the same day as the autocall barrier, then the current coupon is paid. In addition, if you had activated a memory (or snowball) variation of the autocallable, then not only is the current coupon paid but also any previous coupons that were not paid because the underlying had not breached the coupon barrier.
  - If the autocall barrier is hit and if the coupon barrier was set to be paid on the coupon date, then the coupon is not paid. This is true even if the autocall barrier is hit on the coupon observation date.
- Accrual and the autocall barrier is set to be continuously monitored, if the autocall barrier is hit then the accrued coupon up to that date is also paid.

### Memory

You can choose to activate a memory (or snowball) variation of the autocallable. If you choose to do this, on any coupon observation date that the underlying breaches the coupon barrier, then not only is the current coupon paid but also any previous coupons that were not paid because on those coupon dates the underlying did not breach the coupon barrier.

This setting can only be activated if you select the binary coupon style.

### Coupon Style

You can choose whether the coupon style is to be binary or accrued.

If the coupon style is set to:

- Binary, then on each coupon observation date if there is a coupon to be paid and you have:
  - Not activated the memory setting the coupon is calculated as Coupon (tc)
  - You have activated the memory setting the coupon is calculated as Coupon (tc) + (sum of any previous non-paid coupons)
- Accrual, then because the instrument is a type of range accrual, the coupon rate (which is the interest rate that the issuer pays to the investor per coupon) is accrued over the observation period, i.e., the actual coupon period.
  - That is, for each defined fixing date in the coupon period that the underlying on that date fixes equal to or greater than the coupon barrier for this period, the product accrues a portion of the coupon.
  - Accordingly, on each coupon date if there is a coupon to be paid it is calculated as follows:
    ```
    Coupon (tc) * n / N
    ```
    Where:
    - n is the number of fixing dates during the period where the underlying on that date is greater than or equal to this coupon barrier.
    - N is the total number of fixing dates during the period.
  - The period itself is measured from the day after the coupon date prior to this coupon date (or, for the first coupon date only, from the day after the instrument was entered into) up to and including this coupon date.
  - So for example, if the underlying on each fixing date in the coupon period fixes above the coupon barrier throughout the coupon, then the accrual ratio is set to 1 and the whole coupon rate is received.
  - This payment style is not supported if you activate the memory setting.

However, regardless of which style you choose the actual payout calculated is always made on the coupon date, unless the autocall barrier is hit and you have chosen to receive the payment immediately.

### Accrual Frequency

This sets the frequency of the fixing dates on which the system checks if the underlying is above the coupon barrier.

### Coupon

This is the maximum interest rate that the issuer pays to the investor per coupon. It is defined as a percentage of the notional. For example, if it is 5% and the notional is $1m, on each coupon date that a coupon is paid you get 5% of 1m, i.e., $50,000, if the coupon style is binary; if the coupon style is accrual, the amount paid depends of course on how much of the coupon rate was accrued.

You can define a negative coupon rate.

### Notional

This defines the principal. It is the amount on which the coupon rate is paid, and it is the amount repaid by the issuer to the holder either on the maturity date (if the option did not already knock out) or on the coupon date on which the callable event occurred.

## Options at Expiry

The structurer can optionally include up to three "options at expiry".

An option at expiry (which can be either long or short and a call or a put) is an option that can only be exercised on the autocallable's expiry date (the date on which this option itself also automatically expires) and only if there is no early redemption of the autocallable (i.e., the autocall barrier has not been hit and so the product runs to the full investment term).

In SDX Equities supported options at expiry include the following:

- Vanilla
- Asian
  - If you choose to use an Asian option at expiry, you will need to set the underlying of the payout of the options at expiry to Basket.
- Knock in barrier (European or American style)
- Knock out barrier (European or American style)
- No touch
- One touch

Depending on which option at expiry or combination of options at expiry the structurer (or issuer) chooses, this element leads to an additional element of risk or profit for the investor (which in turn affects the premium paid for the autocallable itself by the investor).

This is because if the autocallable reaches the expiry date without being redeemed (i.e., the autocall barrier has not been hit), then as long as the selected options are live on that date (for example, you included a knock out and it has not been knocked out or you included a knock in and it has been knocked in) the investor becomes short or long the selected options. So for example, if the structurer includes:

- A short put, on the expiry date the investor is exposed to the downside of the underlying relative to the strike. Although for a bond autocallable this risk is limited to the redeemed notional, for an option autocallable it is only limited to the strike * notional.
- A long call, on the expiry date the investor will gain from any upside of the underlying in excess of the strike.
- A short call, on the expiry date the investor is exposed to the upside of the underlying market. Although for a bond autocallable this risk is limited to the redeemed notional, for an option autocallable there is no limit.
- A long put, on the expiry date the investor will gain from any downside of the underlying relative to the strike.

Accordingly for each option at expiry the structurer would set the strike relative to the original price of the underlying so as to maximize the risk for the investor (if the investor is entering into a short put or a short call) or to minimize the profit for the investor (if the investor is entering into a long put or a long call).

You define any required options at expiry in the Options at Expiry area using the three Option Class dropdown lists. For each instrument you select, the system displays the relevant fields you need to define.

You can choose to use a combination of these instruments to:

- Create different structures. For example, to define a put spread you will need to define two vanilla puts.
- Gain leverage. For example, if you define a short vanilla put with a strike of 100% and a gearing of 200%, for each 1% that the underlying falls below 100% the payout is reduced by 2%.
- Spread the percentage of the risk across a number of instruments. For example, you can define three instruments, each with a gearing of 33% whose payoff areas (i.e., the areas of underlying in which a payout will occur for each instrument) overlap.

There are a number of options at expiry that you can use. Following are some examples:

### Vanilla put

Choosing this option means that the autocallable investor is short a vanilla option and has in effect committed to settle the vanilla option with the autocallable issuer if on the expiry date the callable event has not occurred.

This vanilla option uses the strike defined in the Strike field and expires immediately on the autocallable's expiry date. In addition, its payout underlying is either the worst performance on the expiry date or the average value of the performance of each asset in the basket on that date, as set in the Underlying of Payout field.

Accordingly on the expiry date, if the autocallable has not yet been redeemed then the redemption amount (which is floored at 0) is calculated as follows:

```
100% - gearing * Downside
```

Where if the underlying of the payout is:
- Worst of, the Downside is Max (0, strike - WorstPerformance[T])
- Basket, the Downside is Max (0, strike - Basket)
  - Basket is the average of R(1), R(2), R(3), ...
  - R(i) is the spot of asset i at time T / initial spot of asset i
  - T is the instrument's expiry date

### Knock in barrier put

Choosing this option means that the autocallable investor is short a knock in barrier option, that the investor has in effect committed to settle a knock in barrier to the autocallable issuer if on the expiry date both of the following conditions are true:

- The callable event has not occurred and
- The worst performance is below the down and in barrier on that date (if it is a European barrier) or was below the down and in barrier at any point during the instrument's lifetime (if it is an American barrier).

Certainly, I'll continue with the markdown conversion:

If the knock in option is knocked in, the underlying vanilla put uses the strike defined in the Strike field and expires immediately on the autocallable's expiry date. In addition, its payout underlying is either the worst performance on the expiry date or the average value of the performance of each asset in the basket on that date as set in the Underlying of Payout field.

Accordingly on the expiry date, if the autocallable has not yet been redeemed then the redemption amount (which is floored at 0):

- For a European style knock in barrier put is calculated as follows: If underlying is equal to or greater than the put barrier, then the redemption amount is 100%. Otherwise the redemption amount is 100% - gearing * Downside.
- For an American style knock in barrier put is calculated as follows: If on any trading day between the valuation date and expiry date the underlying is less than the put barrier, then the redemption amount is 100% - gearing * Downside. Otherwise the redemption amount is 100%.

Where if the underlying of the payout is:
- Worst of, the Downside is Max (0, strike - WorstPerformance[T])
- Basket, the Downside is Max (0, strike - Basket)
  - Basket is the average of R(1), R(2), R(3), ...
  - R(i) is the spot of asset i at time T / initial spot of asset i
  - T is the instrument's expiry date

### Put spread (which consists of two vanilla puts)

Choosing this option means that the autocallable investor is short a put spread vanilla strategy, that the investor has in effect committed to settle a put spread vanilla strategy if on the expiry date the callable event has not occurred.

This put spread option uses the strikes defined in the Strike and Lower Strike fields and expires immediately on the autocallable's expiry date. In addition, its payout underlying is either the worst performance on the expiry date or the average value of the performance of each asset in the basket on that date as set in the Underlying of Payout field.

Accordingly on the expiry date, if the autocallable has not yet been redeemed then the redemption amount (which is floored at 0) is calculated as follows:

```
100% - gearing * Floored Downside
```

Where if the underlying of the payout is:
- Worst of, the Floored Downside is Max { 0, strike - max(lower strike, WorstPerformance[T]) }
- Basket, the Floored Downside is Max { 0, Strike - Max(lower strike, Basket) }
  - Basket is the average of R(1), R(2), R(3), ...
  - R(i) is the spot of asset i at time T / initial spot of asset i
  - T is the instrument's expiry date

## Advantages of an Autocallable

The investor will enter into this instrument to:

1. **Profit from small market moves.**
   - The autocall barrier is usually set at or around the original price of the underlying instrument at the time of issue, that is, around 100%. As a result, even small appreciations (or no movement at all) in the price of the underlying can trigger an early redemption and the payment of high coupons. Therefore there is a real opportunity to realize profits after a short time, with the added benefit of an early redemption event.

2. **Get a better coupon rate than the current market interest rate while ensuring full principal protection as long as the underlying short put is not in-the-money on the expiry date.**
   - This better rate (which is linked to the performance of the underlying) is achieved due to the fact that this instrument has several risks for the investor. These risks are that a coupon will not be paid if the underlying is below the coupon barrier and the fact that the investor is short a put instrument. If this short put instrument is in-the-money on the expiry date the investor can still lose money as in effect the losses incurred by the short put will come out of the principal the investor gets back.

3. **Receive well defined returns, from a broad market view.**
   - Investors can generate a fixed return by taking a very broad view on an underlying. For example, an investor may feel that a particular underlying might appreciate over the next four years but has no strong view on the timing or the size of any increase. By purchasing an autocallable, this investor benefits from an attractive fixed return if this view is correct. That is, as long as the underlying is at or above the autocall barrier on one of the predefined observation dates, the product will be redeemed automatically and the investor will receive the relevant cash amount plus the high coupon.

4. **Lower the "jump risk".**
   - This is true if you enter into an accrual coupon style rather than into a binary coupon style.
   - The investor's assumption is necessarily that the value of the underlying will be above the defined coupon barrier over the coupon period. However, if the value of the underlying is only compared to the coupon barrier on the coupon date and the underlying falls at the very end of the coupon period, the result is that the entire coupon will not be paid. Instead, by accruing the coupon rate over the coupon period, the structure is less risky. By regularly monitoring the value of the underlying relative to the defined coupon barrier, for example, on a daily basis, the investor does not have to make the more difficult prediction of where the underlying will be just on the coupon dates (which is what is required for an binary coupon style of autocallable instrument). Accordingly, even if the value of the underlying does fall at the end of coupon, the investor will still get a payout on the coupon date.

## Defining an Autocallable

In SDX Equities, once you have defined an autocallable in the Single Option page you can then save it directly as a structured product.

To define an autocallable in SDX Equities the following parameters must be set:

### Coupon Barrier

For more information on this parameter see Coupon Barrier.

You can set this barrier to be a European or an American barrier.
- If you enable the Continuous Monitoring feature for the coupon barrier (making it an American barrier), this means that the coupon is more likely to be hit. As a result the instrument will be more expensive.

Although by default the coupon barrier is fixed throughout the life of the bond, you can then change the coupon barrier for each coupon. You do this in the Coupon Dates & Rates window which is accessed by clicking the Coupon Dates & Rates button.

### Autocall Barrier

For more information on this parameter see Autocall Barrier.

You can set this barrier to be a European or an American barrier.
- If you enable the Continuous Monitoring feature for the autocall barrier (making it an American barrier), this means that the coupon is more likely to be hit, increasing the opportunity to realize profits after a short time, with the added benefit of an early redemption event. As a result, the instrument will usually be more expensive.

Although by default the autocall barrier is fixed throughout the life of the bond, you can then change the autocall barrier for each coupon. You do this in the Coupon Dates & Rates window which is accessed by clicking the Coupon Dates & Rates button.

### Coupon

This is the interest rate that the issuer pays to the investor per coupon. It is defined as a percentage of the notional (or principal). For example, if it is 5% and the notional is $1m, on each coupon you get 5% of 1m, i.e., $50,000.

Although by default the coupon rate is fixed throughout the life of the bond, you can then change the coupon rate for each coupon. You do this in the Coupon Dates & Rates window which is accessed by clicking the Coupon Dates & Rates button.

### Notional

This defines the principal. It is the amount on which the coupon rate is paid, and it is the amount repaid by the issuer to the investor either on the expiry date (if the option has not already been knocked out) or on the coupon date on which the autocall barrier is breached.

### Format: Bond <> Option <> Swap

This defines whether the autocallable is wrapped as a Bond or an Option or a Swap.

### Credit Spread

In pricing the bond or option version of this instrument the calculated results depend on the credit spread (or credit worthiness) of the issuer. The credit spread (or credit worthiness) indicates the likelihood that the issuer will not default on either the coupon payments or the return of the notional.

For more information on choosing which type of credit spread curve to use see Defining the Credit Spread.

### Floating Spread

In pricing the swap version of this instrument you must define the floating spread to be used for the underlying cash flows.

In the Floating Spread field you define the spread that will be used by default for each underlying cash flow. However, if you then access the Cash Flow & Dates Window (by clicking the Cash Flow Float button) you can then customize the floating spread for each underlying cash flow individually (as well as see the details for each underlying cash flow). The floating leg's index is automatically set to the default index for the currency.

### Fields for the Options at Expiry

The following fields are used for the options at expiry:

#### Underlying of Payout

This defines the underlying of the payout for the option(s) at expiry and can be either of the following:
- Worst of: In this case, the underlying for the payout calculation is the worst performance on the expiry date.
- Basket: In this case, the underlying for the payout calculation is the equi-weighted average value of the performance of each asset in the basket on the expiry date.

If you include an Asian in the options at expiry, you must set the Underlying of Payout setting to Basket.

#### Strike

This is defined as a percentage of the initial underlying.

#### Barrier

The knock in or knock out trigger, which is only defined for an option at expiry with a barrier, is defined as a percentage of the initial underlying.

If the instrument contains more that one asset, note that the barrier itself can only be triggered by the worst performing asset.

#### Trigger

The trigger, which is only defined for the one touch or the no touch expiry at option, is defined as a percentage of the initial underlying.

If the instrument contains more that one asset, note that the trigger can only be hit by the worst performing asset.

#### Gearing

This defines the notional of each option at expiry. It is defined as a percentage of the autocallable's notional. So for example, if it is set to 50%, then the notional of the short put is 50% of the autocallable's notional.

In addition, you can edit the instrument's fixings in the Accrual Details window; this window is also used to display the Asian's fixing details, if you include an Asian in the options at expiry. For more information on this window see Accrual Details Window.

Once you have priced and calculated an autocallable, in the Single Option page you can then see the probability to hit information for its coupon barrier and (if defined) for its autocall barrier, as well as for any defined options at expiry that contain a barrier. This information is available via the Probability Table link.

## Saving an Autocallable as a Structured Product

In SDX Equities, when you define an autocallable in the Single Option page you can choose to save it as a structured product for future use by yourself and, optionally, other users in your group.

You do this using the fields at the top of this instrument's interface (as seen in Figure 1) in the Single Option page.

You must define a name and then click the Save button. You should note that if you:

- Check the Add to Catalog button, this ensures that the saved autocallable structure will subsequently be available via the Structure Catalog, either via the My Catalog list (if you save it into the Private Folder directory) or the Company Catalog list (if you save it into the Public Folder directory), as well as via the Portfolio Management window.
- Do not check the Add to Catalog button the saved autocallable structure will subsequently only be available via the Portfolio Management window (whether you access this via the Structure Folder button or the Open button).

When you subsequently access this saved structure, it is always opened in the Single Option page.

You cannot access a saved autocallable via the Structured Product Generator window itself.