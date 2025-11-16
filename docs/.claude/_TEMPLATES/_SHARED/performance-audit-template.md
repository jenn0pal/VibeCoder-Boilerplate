# Performance Audit Template

> **Comprehensive performance analysis and optimization guide**

## Audit Information

**Date:** [YYYY-MM-DD]
**Auditor:** [Name]
**Target:** [Application/Feature/Page]
**Environment:** [Production/Staging/Development]
**Tool Stack:** [List tools used]

---

## Performance Budget

### Current Metrics
| Metric | Current | Target | Status |
|--------|---------|--------|--------|
| First Contentful Paint (FCP) | [X]ms | < 1.8s | ✅/❌ |
| Largest Contentful Paint (LCP) | [X]ms | < 2.5s | ✅/❌ |
| First Input Delay (FID) | [X]ms | < 100ms | ✅/❌ |
| Cumulative Layout Shift (CLS) | [X] | < 0.1 | ✅/❌ |
| Time to Interactive (TTI) | [X]ms | < 3.8s | ✅/❌ |
| Total Blocking Time (TBT) | [X]ms | < 200ms | ✅/❌ |

### Lighthouse Scores
- **Performance:** [X]/100 (Target: > 90)
- **Accessibility:** [X]/100 (Target: > 90)
- **Best Practices:** [X]/100 (Target: > 90)
- **SEO:** [X]/100 (Target: > 90)

---

## Frontend Performance

### Bundle Analysis

**Bundle Size:**
| Asset | Size (gzip) | Uncompressed | % of Total |
|-------|-------------|--------------|------------|
| main.js | [X]KB | [Y]KB | [Z]% |
| vendor.js | [X]KB | [Y]KB | [Z]% |
| main.css | [X]KB | [Y]KB | [Z]% |
| **Total** | **[X]KB** | **[Y]KB** | **100%** |

**Issues:**
- [ ] Bundle too large (> 200KB gzipped)
- [ ] Unused code included
- [ ] Large dependencies
- [ ] No code splitting

**Recommendations:**
1. [Specific optimization]
2. [Specific optimization]

### JavaScript Performance

**Execution Time:**
- Main thread blocked: [X]ms
- Long tasks (> 50ms): [N]
- Total JavaScript time: [X]ms

**Issues:**
- [ ] Excessive JavaScript execution
- [ ] Blocking render
- [ ] Unnecessary computations
- [ ] Memory leaks

**Code Quality:**
```javascript
// Example of performance issue found
function slowFunction() {
  // Issue: O(n²) complexity
  for (let i = 0; i < array.length; i++) {
    for (let j = 0; j < array.length; j++) {
      // ...
    }
  }
}

// Optimized version
function fastFunction() {
  // Optimization: O(n) complexity
  const map = new Map();
  for (const item of array) {
    map.set(item.id, item);
  }
}
```

### CSS Performance

**CSS Size:**
- Total CSS: [X]KB (gzipped)
- Unused CSS: [Y]KB ([Z]%)
- Critical CSS: [A]KB

**Issues:**
- [ ] Unused CSS rules
- [ ] Complex selectors
- [ ] No critical CSS inlining
- [ ] Render-blocking stylesheets

**Recommendations:**
1. Purge unused CSS
2. Inline critical CSS
3. Defer non-critical CSS

### Images & Media

**Image Analysis:**
| Image | Size | Format | Optimized? | Recommended |
|-------|------|--------|------------|-------------|
| hero.jpg | [X]KB | JPG | ❌ | WebP, lazy load |
| logo.png | [X]KB | PNG | ❌ | SVG |

**Issues:**
- [ ] Unoptimized images
- [ ] Wrong image format
- [ ] Missing lazy loading
- [ ] No responsive images
- [ ] No CDN usage

**Recommendations:**
1. Convert to WebP/AVIF
2. Implement lazy loading
3. Use responsive images (`srcset`)
4. Serve from CDN

### Fonts

**Font Loading:**
- Font files: [N]
- Total font size: [X]KB
- FOIT/FOUT: [Observed behavior]

**Issues:**
- [ ] Blocking font loading
- [ ] Too many font weights
- [ ] No font subsetting
- [ ] No font preloading

**Recommendations:**
1. Use `font-display: swap`
2. Preload critical fonts
3. Subset fonts
4. Limit font variations

---

## Backend Performance

### API Response Times

| Endpoint | Avg (ms) | P50 (ms) | P95 (ms) | P99 (ms) | Status |
|----------|----------|----------|----------|----------|--------|
| GET /api/users | [X] | [X] | [X] | [X] | ✅/❌ |
| POST /api/auth | [X] | [X] | [X] | [X] | ✅/❌ |
| GET /api/data | [X] | [X] | [X] | [X] | ✅/❌ |

**Target:** P95 < 200ms for most endpoints

**Issues:**
- [ ] Slow database queries
- [ ] N+1 query problem
- [ ] Missing indexes
- [ ] No caching
- [ ] Unnecessary data fetching

### Database Performance

**Query Analysis:**
```sql
-- Slow query example
EXPLAIN ANALYZE
SELECT * FROM users
JOIN posts ON users.id = posts.user_id
WHERE users.created_at > '2024-01-01';

-- Results:
-- Execution time: [X]ms
-- Rows scanned: [N]
-- Index used: [Yes/No]
```

**Issues:**
- [ ] Full table scans
- [ ] Missing indexes
- [ ] N+1 queries
- [ ] Inefficient joins
- [ ] No query caching

**Recommendations:**
1. Add indexes on [columns]
2. Use eager loading for [relations]
3. Implement query caching
4. Optimize join strategy

### Caching

**Cache Hit Rates:**
| Cache Layer | Hit Rate | Misses/hour | Evictions/hour |
|-------------|----------|-------------|----------------|
| Redis (app) | [X]% | [N] | [N] |
| Browser cache | [X]% | [N] | - |
| CDN cache | [X]% | [N] | [N] |

**Issues:**
- [ ] Low cache hit rate (< 80%)
- [ ] Inappropriate TTLs
- [ ] No cache invalidation strategy
- [ ] Missing cache layers

### Server Resources

**Resource Utilization:**
| Resource | Current | Peak | Threshold | Status |
|----------|---------|------|-----------|--------|
| CPU | [X]% | [Y]% | < 70% | ✅/❌ |
| Memory | [X]GB | [Y]GB | < [Z]GB | ✅/❌ |
| Disk I/O | [X] ops/s | [Y] ops/s | < [Z] | ✅/❌ |
| Network | [X] MB/s | [Y] MB/s | < [Z] | ✅/❌ |

**Issues:**
- [ ] CPU spikes during peak hours
- [ ] Memory leaks
- [ ] High disk I/O
- [ ] Network bottlenecks

---

## Network Performance

### Request Waterfall

**Critical Path:**
1. HTML: [X]ms
2. CSS: [X]ms (blocking)
3. JS: [X]ms (blocking)
4. API call: [X]ms
5. Render: [X]ms

**Total:** [X]ms

**Issues:**
- [ ] Too many requests ([N] requests)
- [ ] Render-blocking resources
- [ ] Large request chain
- [ ] No HTTP/2 or HTTP/3
- [ ] No request prioritization

### Connection Performance

- **Round-trip time (RTT):** [X]ms
- **TLS handshake:** [X]ms
- **DNS lookup:** [X]ms
- **TCP connection:** [X]ms

**Issues:**
- [ ] High latency
- [ ] Slow DNS resolution
- [ ] No keep-alive
- [ ] No connection pooling

---

## Mobile Performance

### Mobile Metrics
| Device | Load Time | FCP | LCP | CLS |
|--------|-----------|-----|-----|-----|
| 4G Mobile | [X]s | [X]ms | [X]ms | [X] |
| 3G Mobile | [X]s | [X]ms | [X]ms | [X] |

**Issues:**
- [ ] Poor mobile performance
- [ ] No mobile optimization
- [ ] Large resources for mobile
- [ ] No adaptive loading

---

## Optimization Recommendations

### Priority 1 (High Impact, Quick Wins)
1. **[Optimization]**
   - Impact: [Estimated improvement]
   - Effort: [Low/Medium/High]
   - Implementation: [Steps]

2. **[Optimization]**
   - Impact: [Estimated improvement]
   - Effort: [Low/Medium/High]
   - Implementation: [Steps]

### Priority 2 (High Impact, More Effort)
1. **[Optimization]**
2. **[Optimization]**

### Priority 3 (Nice to Have)
1. **[Optimization]**
2. **[Optimization]**

---

## Monitoring Setup

### Metrics to Track
- [ ] Core Web Vitals (LCP, FID, CLS)
- [ ] API response times
- [ ] Error rates
- [ ] Database query times
- [ ] Cache hit rates
- [ ] Server resource usage

### Tools
- [ ] **Real User Monitoring (RUM):** [Tool name]
- [ ] **Synthetic Monitoring:** [Tool name]
- [ ] **APM:** [Tool name]
- [ ] **Error Tracking:** [Tool name]

### Alerts
- [ ] LCP > 2.5s
- [ ] API response time > 500ms
- [ ] Error rate > 1%
- [ ] CPU > 80%
- [ ] Memory > 90%

---

## Action Plan

### Immediate Actions (This Week)
- [ ] [Action 1 - Owner: Name - Due: Date]
- [ ] [Action 2 - Owner: Name - Due: Date]

### Short-term (This Month)
- [ ] [Action 1]
- [ ] [Action 2]

### Long-term (This Quarter)
- [ ] [Action 1]
- [ ] [Action 2]

---

## Success Metrics

**Target Improvements:**
| Metric | Before | Target | After | Achieved? |
|--------|--------|--------|-------|-----------|
| LCP | [X]ms | < 2.5s | [Y]ms | ✅/❌ |
| Bundle size | [X]KB | < [Y]KB | [Z]KB | ✅/❌ |
| API p95 | [X]ms | < 200ms | [Y]ms | ✅/❌ |

**ROI:**
- Bounce rate reduction: [X]%
- Conversion rate increase: [Y]%
- User satisfaction: [Z]/10

---

## Tooling Reference

### Analysis Tools
- **Lighthouse:** https://developers.google.com/web/tools/lighthouse
- **WebPageTest:** https://www.webpagetest.org/
- **Chrome DevTools:** Performance, Network, Coverage tabs
- **Bundle Analyzer:** webpack-bundle-analyzer, rollup-plugin-visualizer

### Monitoring Tools
- **Google Analytics:** Real user metrics
- **New Relic / DataDog / Dynatrace:** APM
- **Sentry:** Error tracking with performance

---

*Schedule performance audits quarterly or after major releases.*
