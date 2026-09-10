> ## Documentation Index
> Fetch the complete documentation index at: https://resend.com/docs/llms.txt
> Use this file to discover all available pages before exploring further.

# Domain and/or IP Warm-up Guide

> Learn how to warm up a domain or IP to avoid deliverability issues.

export const WarmupCalculator = () => {
  const getToday = () => new Date().toISOString().split('T')[0];
  const [domainType, setDomainType] = useState('new');
  const [targetVolume, setTargetVolume] = useState(5000);
  const [targetDate, setTargetDate] = useState('');
  const [startDate, setStartDate] = useState(getToday);
  const [isInitialized, setIsInitialized] = useState(false);
  useEffect(() => {
    const params = new URLSearchParams(window.location.search);
    if (params.get('type') === 'existing') setDomainType('existing');
    const volumeParam = Number(params.get('volume'));
    if (!Number.isNaN(volumeParam) && volumeParam >= 100) setTargetVolume(volumeParam);
    if (params.get('target')) setTargetDate(params.get('target'));
    if (params.get('start')) setStartDate(params.get('start'));
    setIsInitialized(true);
  }, []);
  useEffect(() => {
    if (!isInitialized) return;
    const params = new URLSearchParams();
    const today = getToday();
    if (domainType !== 'new') params.set('type', domainType);
    if (targetVolume !== 5000) params.set('volume', String(targetVolume));
    if (targetDate) params.set('target', targetDate);
    if (startDate !== today) params.set('start', startDate);
    const newUrl = params.toString().length > 0 ? `${window.location.pathname}?${params.toString()}` : window.location.pathname;
    window.history.replaceState({}, '', newUrl);
  }, [domainType, targetVolume, targetDate, startDate, isInitialized]);
  const roundVolume = value => {
    if (value >= 3000) {
      return Math.ceil(value / 500) * 500;
    }
    return Math.ceil(value / 100) * 100;
  };
  const newDomainBase = [{
    day: 1,
    daily: 150,
    hourly: null
  }, {
    day: 2,
    daily: 250,
    hourly: null
  }, {
    day: 3,
    daily: 400,
    hourly: null
  }, {
    day: 4,
    daily: 700,
    hourly: 50
  }, {
    day: 5,
    daily: 1000,
    hourly: 75
  }, {
    day: 6,
    daily: 1500,
    hourly: 100
  }, {
    day: 7,
    daily: 2000,
    hourly: 150
  }];
  const existingDomainBase = [{
    day: 1,
    daily: 1000,
    hourly: 100
  }, {
    day: 2,
    daily: 2500,
    hourly: 300
  }, {
    day: 3,
    daily: 5000,
    hourly: 600
  }, {
    day: 4,
    daily: 5000,
    hourly: 800
  }, {
    day: 5,
    daily: 7500,
    hourly: 1000
  }, {
    day: 6,
    daily: 7500,
    hourly: 1500
  }, {
    day: 7,
    daily: 10000,
    hourly: 2000
  }];
  const formatDate = (dateStr, addDays = 0) => {
    const [year, month, day] = dateStr.split('-').map(Number);
    const date = new Date(year, month - 1, day);
    date.setDate(date.getDate() + addDays);
    return date.toLocaleDateString('en-US', {
      month: 'short',
      day: 'numeric',
      year: 'numeric'
    });
  };
  const getDaysBetween = (start, end) => {
    const startD = new Date(start);
    const endD = new Date(end);
    const diffTime = endD - startD;
    return Math.ceil(diffTime / (1000 * 60 * 60 * 24));
  };
  const schedule = useMemo(() => {
    const baseSchedule = domainType === 'new' ? newDomainBase : existingDomainBase;
    const baseMax = baseSchedule[baseSchedule.length - 1].daily;
    if (targetVolume <= baseMax) {
      return baseSchedule.map(item => ({
        ...item,
        date: formatDate(startDate, item.day - 1)
      }));
    }
    const result = baseSchedule.map(item => ({
      ...item,
      date: formatDate(startDate, item.day - 1)
    }));
    const growthRate = domainType === 'new' ? 1.4 : 1.5;
    let currentDay = 8;
    let currentDaily = baseMax;
    let currentHourly = baseSchedule[baseSchedule.length - 1].hourly;
    while (currentDaily < targetVolume && currentDay <= 42) {
      currentDaily = Math.min(roundVolume(currentDaily * growthRate), targetVolume);
      currentHourly = roundVolume(currentDaily / 10);
      result.push({
        day: currentDay,
        daily: currentDaily,
        hourly: currentHourly,
        date: formatDate(startDate, currentDay - 1)
      });
      currentDay++;
    }
    return result;
  }, [domainType, targetVolume, startDate]);
  const daysNeeded = schedule.length;
  const availableDays = targetDate ? getDaysBetween(startDate, targetDate) : null;
  const isTimelineTooShort = availableDays !== null && availableDays < daysNeeded;
  const recommendedEndDate = formatDate(startDate, daysNeeded - 1);
  return <div className="mt-6 mb-8">
      {}
      <div className="p-6 rounded-xl border border-zinc-500/20 bg-zinc-50/50 dark:border-zinc-500/30 dark:bg-zinc-500/10 mb-6">
        <div className="grid gap-5 grid-cols-1 sm:grid-cols-2 lg:grid-cols-3">
          {}
          <div className="sm:col-span-2 lg:col-span-3">
            <span className="block mb-1.5 font-medium text-sm">
              Domain Type
            </span>
            <div className="flex gap-3 flex-wrap">
              <label className={`flex items-center relative text-sm leading-6 h-9 pl-3.5 pr-4 rounded-xl transition-all ring-1 ${domainType === 'new' ? 'bg-primary/10 text-primary dark:text-primary-light dark:bg-primary-light/10 ring-primary' : 'bg-background-light dark:bg-background-dark dark:brightness-[1.1] ring-gray-400/30 hover:bg-gray-400/20 dark:hover:bg-gray-800/50 hover:ring-gray-600/30 dark:ring-gray-600/30 dark:hover:ring-gray-500/30'}`}>
                <input type="radio" name="domainType" value="new" checked={domainType === 'new'} onChange={e => setDomainType(e.target.value)} className="opacity-0 absolute inset-0 cursor-pointer" />
                <span>New Domain</span>
              </label>
              <label className={`flex items-center relative text-sm leading-6 h-9 pl-3.5 pr-4 rounded-xl transition-all ring-1 ${domainType === 'existing' ? 'bg-primary/10 text-primary dark:text-primary-light dark:bg-primary-light/10 ring-primary' : 'bg-background-light dark:bg-background-dark dark:brightness-[1.1] ring-gray-400/30 hover:bg-gray-400/20 dark:hover:bg-gray-800/50 hover:ring-gray-600/30 dark:ring-gray-600/30 dark:hover:ring-gray-500/30'}`}>
                <input type="radio" name="domainType" value="existing" checked={domainType === 'existing'} onChange={e => setDomainType(e.target.value)} className="opacity-0 absolute inset-0 cursor-pointer" />
                <span>Existing Domain</span>
              </label>
            </div>
          </div>

          {}
          <div>
            <label className="block mb-1.5 font-medium text-sm" htmlFor="targetVolume">
              Target Daily Volume
            </label>
            <input id="targetVolume" type="number" min="100" max="1000000" step="100" value={targetVolume} onChange={e => setTargetVolume(Number(e.target.value))} className="rounded-xl w-full text-sm leading-6 h-9 pl-3.5 pr-3 text-gray-500 dark:text-white/50 bg-background-light dark:bg-background-dark dark:brightness-[1.1] dark:ring-1 dark:hover:brightness-[1.25] ring-1 ring-gray-400/30 hover:ring-gray-600/30 dark:ring-gray-600/30 dark:hover:ring-gray-500/30 transition-all" placeholder="e.g., 5000" />
          </div>

          {}
          <div>
            <label className="block mb-1.5 font-medium text-sm" htmlFor="startDate">
              Start Date
            </label>
            <input id="startDate" type="date" value={startDate} onChange={e => setStartDate(e.target.value)} className="rounded-xl w-full text-sm leading-6 h-9 pl-3.5 pr-3 text-gray-500 dark:text-white/50 bg-background-light dark:bg-background-dark dark:brightness-[1.1] dark:ring-1 dark:hover:brightness-[1.25] ring-1 ring-gray-400/30 hover:ring-gray-600/30 dark:ring-gray-600/30 dark:hover:ring-gray-500/30 transition-all" />
          </div>

          {}
          <div>
            <label className="block mb-1.5 font-medium text-sm" htmlFor="targetDate">
              Target Date (optional)
            </label>
            <input id="targetDate" type="date" value={targetDate} onChange={e => setTargetDate(e.target.value)} min={startDate} className="rounded-xl w-full text-sm leading-6 h-9 pl-3.5 pr-3 text-gray-500 dark:text-white/50 bg-background-light dark:bg-background-dark dark:brightness-[1.1] dark:ring-1 dark:hover:brightness-[1.25] ring-1 ring-gray-400/30 hover:ring-gray-600/30 dark:ring-gray-600/30 dark:hover:ring-gray-500/30 transition-all" />
          </div>
        </div>
      </div>

      {}
      {isTimelineTooShort && <div className="my-4 px-5 py-4 overflow-hidden rounded-2xl flex gap-3 border border-amber-500/20 bg-amber-50/50 dark:border-amber-500/30 dark:bg-amber-500/10">
          <div className="mt-0.5 w-4 flex-none">
            <svg className="w-5 h-5 text-amber-400 dark:text-amber-300/80" fill="none" viewBox="0 0 24 24" stroke="currentColor" strokeWidth="2" role="img" aria-label="Warning">
              <title>Warning</title>
              <path strokeLinecap="round" strokeLinejoin="round" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
            </svg>
          </div>
          <div className="text-sm min-w-0 w-full text-amber-900 dark:text-amber-200">
            Your target date allows for {availableDays} days, but a safe warm-up
            requires at least {daysNeeded} days to reach{' '}
            {targetVolume.toLocaleString()} emails/day. Consider setting your
            target date to{' '}
            <strong>{formatDate(startDate, daysNeeded - 1)}</strong> or later,
            or adjusting your target volume.
          </div>
        </div>}

      {}
      <div className="p-4 rounded-lg border border-zinc-500/20 bg-zinc-50/50 dark:border-zinc-500/30 dark:bg-zinc-500/10 mb-4">
        <div className="flex flex-wrap gap-6 justify-between">
          <div>
            <div className="text-xs opacity-70 mb-1">Warm-up Duration</div>
            <div className="text-xl font-semibold">{daysNeeded} days</div>
          </div>
          <div>
            <div className="text-xs opacity-70 mb-1">Start Date</div>
            <div className="text-xl font-semibold">{formatDate(startDate)}</div>
          </div>
          <div>
            <div className="text-xs opacity-70 mb-1">Full Capacity Date</div>
            <div className="text-xl font-semibold">{recommendedEndDate}</div>
          </div>
          <div>
            <div className="text-xs opacity-70 mb-1">Target Volume</div>
            <div className="text-xl font-semibold">
              {targetVolume.toLocaleString()}/day
            </div>
          </div>
        </div>
      </div>

      {}
      <div data-table-wrapper="true" className="[--page-padding:20px] overflow-x-auto flex w-[calc(100%+(var(--page-padding)*2))] my-[1em] py-[1em] -mx-[var(--page-padding)] max-w-none [contain:inline-size]">
        <div className="px-[var(--page-padding)] grow max-w-none w-full">
          <div role="table" aria-label="Warm-up schedule" className="grid w-max max-w-full gap-x-4 gap-y-2 text-sm" style={{
    gridTemplateColumns: 'repeat(4, max-content)'
  }}>
            <div role="columnheader" className="text-left font-semibold whitespace-nowrap">
              <strong>Day</strong>
            </div>
            <div role="columnheader" className="text-left font-semibold">
              <strong>Date</strong>
            </div>
            <div role="columnheader" className="text-left font-semibold">
              <strong>Messages per day</strong>
            </div>
            <div role="columnheader" className="text-left font-semibold">
              <strong>Messages per hour</strong>
            </div>
            {schedule.map(row => <div key={row.day} role="row" className="contents">
                <div role="cell" className="tabular-nums whitespace-nowrap font-semibold text-left md:pr-8">
                  <strong>{row.day}</strong>
                </div>
                <div role="cell" className="text-left md:pr-8">
                  {row.date}
                </div>
                <div role="cell" className="text-left md:pr-8">
                  Up to {row.daily.toLocaleString()} emails
                </div>
                <div role="cell" className="text-left md:pr-8">
                  {row.hourly ? `${row.hourly.toLocaleString()} Maximum` : '—'}
                </div>
              </div>)}
          </div>
        </div>
      </div>

      {}
      <div className="my-4 px-5 py-4 overflow-hidden rounded-2xl flex gap-3 border border-emerald-500/20 bg-emerald-50/50 dark:border-emerald-500/30 dark:bg-emerald-500/10">
        <div className="mt-0.5 w-4 flex-none">
          <svg width="11" height="14" viewBox="0 0 11 14" fill="currentColor" xmlns="http://www.w3.org/2000/svg" className="text-emerald-600 dark:text-emerald-400/80 w-3.5 h-auto" role="img" aria-label="Tip">
            <title>Tip</title>
            <path d="M3.12794 12.4232C3.12794 12.5954 3.1776 12.7634 3.27244 12.907L3.74114 13.6095C3.88471 13.8248 4.21067 14 4.46964 14H6.15606C6.41415 14 6.74017 13.825 6.88373 13.6095L7.3508 12.9073C7.43114 12.7859 7.49705 12.569 7.49705 12.4232L7.50055 11.3513H3.12521L3.12794 12.4232ZM5.31288 0C2.52414 0.00875889 0.5 2.26889 0.5 4.78826C0.5 6.00188 0.949566 7.10829 1.69119 7.95492C2.14321 8.47011 2.84901 9.54727 3.11919 10.4557C3.12005 10.4625 3.12175 10.4698 3.12261 10.4771H7.50342C7.50427 10.4698 7.50598 10.463 7.50684 10.4557C7.77688 9.54727 8.48281 8.47011 8.93484 7.95492C9.67728 7.13181 10.1258 6.02703 10.1258 4.78826C10.1258 2.15486 7.9709 0.000106649 5.31288 0ZM7.94902 7.11267C7.52078 7.60079 6.99082 8.37878 6.6077 9.18794H4.02051C3.63739 8.37878 3.10743 7.60079 2.67947 7.11294C2.11997 6.47551 1.8126 5.63599 1.8126 4.78826C1.8126 3.09829 3.12794 1.31944 5.28827 1.3126C7.2435 1.3126 8.81315 2.88226 8.81315 4.78826C8.81315 5.63599 8.50688 6.47551 7.94902 7.11267ZM4.87534 2.18767C3.66939 2.18767 2.68767 3.16939 2.68767 4.37534C2.68767 4.61719 2.88336 4.81288 3.12521 4.81288C3.36705 4.81288 3.56274 4.61599 3.56274 4.37534C3.56274 3.6515 4.1515 3.06274 4.87534 3.06274C5.11719 3.06274 5.31288 2.86727 5.31288 2.62548C5.31288 2.38369 5.11599 2.18767 4.87534 2.18767Z" />
          </svg>
        </div>
        <div className="text-sm min-w-0 w-full text-emerald-900 dark:text-emerald-200">
          As you warm up, keep your <strong>bounce rate below 4%</strong> and
          your <strong>spam rate below 0.08%</strong>. If these rates increase,
          slow down your warm-up and investigate the root cause before
          continuing.
        </div>
      </div>
    </div>;
};

Warming up a domain or IP refers to the practice of progressively increasing your sending volume to maximize your deliverability. The goal is to send at a consistent rate and avoid any spikes in email volume that might be concerning to inbox service providers.

Whenever you change your sending patterns, warm up your domain and/or IP. This applies when you use a new domain, a new IP, or a new vendor, or when your volume will increase.

A thought-out warm-up plan limits greylisting and delivery throttling, as well as helping establish a good domain and IP reputation.

As your volume increases, you'll need to monitor your bounce rate to ensure it remains below 4%, and your spam rate below 0.08%. An increase in these rates would be a sign that your warm-up plan needs to be slowed down and an investigation into the root causes of the increases started.

Following these rules and metrics will establish a good domain reputation.

<Info>
  Each sender has different constraints and needs, so these numbers are meant as
  a baseline. Our [Support team](https://resend.com/help) can work with you on
  devising a plan adapted to your needs.
</Info>

## Existing domain

If you're already sending from an existing domain with established reputation and volumes, you can use the following guidelines to start sending with Resend.

| **Day** | **Messages per day** | **Messages per hour** |
| ------- | -------------------- | --------------------- |
| **1**   | Up to 1,000 emails   | 100 Maximum           |
| **2**   | Up to 2,500 emails   | 300 Maximum           |
| **3**   | Up to 5,000 emails   | 600 Maximum           |
| **4**   | Up to 5,000 emails   | 800 Maximum           |
| **5**   | Up to 7,500 emails   | 1,000 Maximum         |
| **6**   | Up to 7,500 emails   | 1,500 Maximum         |
| **7**   | Up to 10,000 emails  | 2,000 Maximum         |

## New domain

Before you start sending emails with a brand new domain, it's especially important to have a warm-up plan so you can maximize your deliverability right from the start.

| **Day** | **Messages per day** | **Messages per hour** |
| ------- | -------------------- | --------------------- |
| **1**   | Up to 150 emails     |                       |
| **2**   | Up to 250 emails     |                       |
| **3**   | Up to 400 emails     |                       |
| **4**   | Up to 700 emails     | 50 Maximum            |
| **5**   | Up to 1,000 emails   | 75 Maximum            |
| **6**   | Up to 1,500 emails   | 100 Maximum           |
| **7**   | Up to 2,000 emails   | 150 Maximum           |

## Warm-up calculator

Use the calculator below to generate a personalized warm-up schedule based on your specific needs. Enter your target volume, timeline, and domain type to get a custom plan.

The guide is meant as a general plan, but always pay careful attention to your deliverability and adjust accordingly. If you have specific questions, [please reach out to us](https://resend.com/help).

<WarmupCalculator />

# Warming up your Dedicated IP with Resend

In order for a Dedicated IP to be beneficial or useful, you first need to establish a certain sending volume and patterns. Once you've established this volume and these patterns, our [Support team](https://resend.com/help) can set it up for you.

Resend provides an automatic warm-up process so that you can focus on sending.

[Learn more about requesting a Dedicated IP](https://resend.com/docs/knowledge-base/how-do-dedicated-ips-work#how-to-request-a-dedicated-ip).

# Third-party warm-up services

Email deliverability is important, and it can be tempting to use services promising quick fixes. However, using tools that artificially boost engagement can harm your long-term sender reputation. These services often rely on manipulating anti-spam filters, which can backfire as email providers like Gmail adjust their systems.

Instead, focus on sustainable practices, such as sending relevant content, maintaining a clean list, and using proper authentication. These methods build trust with email providers and improve your deliverability over time.
